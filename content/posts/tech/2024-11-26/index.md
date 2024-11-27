---
title: "RDMA and ProRes Video or: How I Learned To Hate Windows Even More"
date: 2024-11-26T13:22:25-05:00
categories: ["tech"]
tags: ["infiniband", "linux", "prores", "windows"]
---

### Intro

This blog post is highly technical and long. I expect people to get bored of this because of its EXTREMELY niche use case. However, for those interested, if you stick around, you may find this worthwhile.

### Background

Streaming is a time sink hobby that I particularly enjoy. It essentially allows you to live demo your skillsets for random NPCs that follow the content you are engaging in. Twitch is my main streaming site and I obviously plug my channel at the end of every post as a templated footer. Most of you will see the recordings on YouTube or my livestream for consumption, but before uploading, there is the still the matter of processing.

The main issue with recording that most people run into is that when recording inside a program like OBS, most guides recommend recording to `h.264` or `h.265` formats, dependent on hardware. This will suffice for a majority of users, since recording is normally associated with a straight upload to video websites that ingest this format.

I'm not the majority.

This section could easily devolve into a black hole, but essentially the most important priority for me in video editing is having the highest quality master copy, of which all my delivery files are based off of. This basically leaves out all video formats that utilize extensive video compression. I needed a file format for my master recording that gives me a visually appealing master copy and that would not tax my CPU. The CPU I use is an `AMD Ryzen 5950X`, but because I record AND stream concurrently, the file format would need to be efficient on the CPU front to not slow down encoding of my stream or the user experience of actually streaming. ProRes meets these requirements, at the cost of filesize. The format of my video is `1920x1080@60FPS`. A `2TB` SATA drive can easily handle this requirement, and most people opt to go this route.

Again, I'm not most people.

When I stream poker, I don't like to take too much of a break in between streams. I came up with the idea of utilizing a network share that could handle at most, four concurrent streams of `1920x1080@60FPS` streams in ProRes format. When you deal with hundreds of `GBs`, you start to notice that you generate the information faster than you can transfer it. I quickly realized I needed to address the interconnect issue and deal with storage requirements later on.

### RDMA decisions

There are multiple RDMA technologies that allow a low latency/high throughput connection. The two competing standards I researched were Infiniband (IB) and RDMA over Converged Ethernet (RoCE). I chose Infiniband because it is the lower latency technology. I want to be limited by disk write speed. I noticed that on eBay I could get a few ConnectX 4.0 cards (VPI specific) and 100Gbps cable and essentially be writing at PCIe 4.0 speed. I also only need to do this via a point to point connection. I wanted to use Thunderbolt initially, but ran into problems with unsupported configurations. IB was perfect, as it has great Linux support at a fast tranfer speed dependent on cable rating. I am also thinking about `3840x2160@60fps` speed. I want to be able to edit these type of masters eventually and future proof my setup. This makes `100Gbps (EDR rating)` extremely cost effective.

### System layout

I love to virtualize everything. I'm writing this blog post on a virtualized desktop actually. The following diagram showcases my physical setup:

```goat {class="ibsetup" caption="IB setup"}
+---------------+                   +-------------+
| VIRT STATION  |-------------------|   DESKTOP   |
+---------------+    EDR CABLE      +-------------+
```

This point to point connection is what transfers my ProRes Videos.

Logically is where things get complicated. I have the following:

- Virt station that runs Arch Linux for KVM/Qemu virtualization. ConnectX 4.0 card is inserted here.
  - AlmaLinux 9.X VM that has an SRIOV Mellanox virtual card
- Windows OS on Desktop (for simplicity)

What can I say? I love to get my money's worth.

### Implementation

I needed to meet the following requirements to get this setup working:

Virt Station

1. Mellanox card inserted into virt station and showing proper initialization.
2. Mellanox SRIOV entries being properly passed through into AlmaLinux.
3. Enabling IB kernel support
4. Activating SR-IOV functionality via Subnet manager
5. Some type of RDMA sharing solution

Desktop

1. Mellanox card being detected by the OS.
2. RDMA verification


### Virt station

Inserting the card was a success. We were able to get the OS to detect the card:

```bash
$ lspci | grep Mel
11:00.0 Infiniband controller: Mellanox Technologies MT27700 Family [ConnectX-4]
```

Now onto SR-IOV. A quick definition from RedHat Documentation:

> The SR-IOV allows different virtual machines (VMs) in a virtual environment to share a single PCI Express hardware interface.
>
> [Source](https://en.wikipedia.org/wiki/Single-root_input/output_virtualization)

This would allow me to insert a virtual function inside a virtual machine to share the ConnectX-4 card. This is where the first issues began. You need to do two things to get the card working in this mode:

1. Enable SR-IOV on the firmware
2. Activate SR-IOV functionality on the card.

SR-IOV functionality can be enabled via tooling or at boot inside the card's firmware. The second, however, is only possible either by using a binary driver or configuring the virtual functions at boot time. I had no idea how to do this at first. However, after a few google searches, it appears we need to do the following:

1. Set up virtual functions via /proc calls
2. Setup GUIDs to differentiate each virtual function (similar to MAC addresses)
3. Assign these virtual functions to pci-vfio driver

I wrote a few scripts that accomplish these operations. You can access them here:

[Infiniband Scripts](https://github.com/dcontiveros/code-snippets/tree/main/infiniband)

The scripts are commented heavily to make it easy to follow, but they do the following:

```python
# set_cx4_guids.sh
# GUID format: AA:BB:{Regular Mac Address}
# EX: AB:CD:00:1A:2B:3C:4D:5E (8 pairs, 16 Hex digits)
1. Specifies GUIDs
2. Creates virtual functions based on the card's entry in lspci
3. Sets node guid based on above format
4. Sets port guid based on above format
5. Sets state to auto for data rate negotiation based on cable

# assign_cx4_vfio.sh
1. Scans for VFs
2. Initializes them
3. Prompts to assign to vfio (useful for checking if the VFs are good)
4. Reassigns the driver from kernel default to vfio-pci
```

This took quite a while to get working. Reddit helped immensely. After specifying the virtual function as a vfio device in qemu, I was able to see it in the OS and enabled IB by following the ArchLinux Infiniband wiki page.

In order for SR-IOV GUIDs to be valid, you need to enable virtualization support on the subnet manager. OpenSM does NOT support virtualization. I commented on this issue on GitHub and received the confirmation:

[OpenSM: Add information about Limitations #22](https://github.com/linux-rdma/opensm/issues/22)

Since I didn't feel like buying an IB switch, I installed the proprietary Subnet Manager from Nvidia/Mellanox, enabled virtualization, and immediately saw connectivity via `ibstat` command. I confirmed connectivity between my actual hardware and my VM via `ibping` and various other diagnostic commands. I was certain connectivity was good inside my virt station.

Now we needed to decide on a fileshare mechanism. I have an additional NVMe drive passed through to the AlmaLinux VM that also had the VF from the ConnectX-4 card. After careful consideration, I decided on SMB Direct as the transport mechanism. Most of my long-length videos occur on Windows when I'm streaming/recording poker. Therefore, I needed a protocol that Windows could use with ease that was RDMA enabled. Some rumblings online pointed me to SMB Direct. Unfortunately, you need to run Windows Server to get this functionality working. Or so I thought.

On further investigation, it turns out that `ksmbd (SMB3 Kernel Server)` built into the Linux kernel has SMB direct support. This is different from SMB Multichannel. SMB Direct bypasses the TCP/IP stack allowing RDMA functionality on transfers. This is what I needed.

I recompiled the Linux kernel from source on AlmaLinux, enabled the module, and started the daemon. I didn't receive any errors, so now it was just a matter of getting the Windows side to connect.

### Desktop

Windows ability to interact with a ConnectX-4 card isn't too difficult. You need to meet the following requirements:

1. Windows Pro For Workstations needs to be installed (Even regular Pro didn't have support when I tried)
2. Drivers
3. IPoIB enabled (this should happen by default)

Most of these steps are self explanatory so I won't go into detail on how I enabled support. This is fairly plug and play, which I appreciated Windows for, since it was similar to downloading GPU drivers.

I was able to ping/connect to the virtual machine after a few tries. However, I noticed that RDMA was NOT enabled. Fortunately I was able to find a fix on the level1techs forum. Apparently, ksmbd was so new that the kernel did not send the correct RDMA flags to the client to actually enable the connection. The GitHub issue where this was reported is here:

[ksmbd Issue #456](https://github.com/namjaejeon/ksmbd/issues/456)

I applied the patch provided and I was immediately presented with True:

```bash
> Get-SmbMultichannelConnection

Server Name Selected Client IP Server IP  Client Interface Index Server Interface Index Client RSS Capable Client RDMA Capable
----------- -------- --------- ---------  ---------------------- ---------------------- ------------------ -------------------
10.0.0.104  True     10.0.0.8  10.0.0.104 8                      1                      False              False
10.0.0.101  True     10.0.1.2  10.0.1.1   17                     3                      False              True
10.0.1.1    True     10.0.1.2  10.0.1.1   17                     3                      False              True
```

The internet is amazing sometimes.

### Limitations

Besides the STEEP learning curve, the only limitation I have now is actually verifying I can write more than 10Gbps of data onto the medium. NVMe drives (consumer drives) are only fast because they have a write cache. When choosing an NVMe drive, what I need is Sustained Write Performance. Therefore, it is important to view benchmarks of drives that take the time to fill up the cache to get the true write speed. Until I upgrade my remote storage, I will not even begin to come close to the speeds RDMA provides. Guess I know what my expense will be.

It is fairly amazing to write this much data and notice zero CPU load due to TCP/IP processing or even write operations.


### Alternate Title

So what about this made me hate Windows even more? I did say that the desktop part was the easiest part of this entire exercise. Well wait not so fast. There are a few reasons why Windows is fairly terrible for this:

1. RDMA support gatekeeping
2. Reliance of IPoIB to create the connectivity
3. General lack of documentation in regards to SMB Direct validation

RDMA support is not enabled on most Windows installations. I had to relicense one of my VMs to Windows 11 Pro for Workstations. I remember during testing I ran a command to confirm RDMA was turned on. It was not. I then relicensed the product, and it magically flipped the option. I suppose not everyone needs RDMA, but locking down access via licensing is just plain idiotic, especially when support is already baked into the kernel.

The overall reliance of IPoIB on the Windows side to initiate connectivity is absurd. Most of the Infiniband functionality isn't directly supported and thus the driver/support hunt always needs to be done on the Windows side. Ideally, I'd like to see something like `libibverbs` in a Windows package enabled. The platform of Infiniband is generally not well documented so having to read years old website posts and seeing they are still applicable is genuinely frustrating, which leads me to my third point overall.

Microsoft does not release any definitive documentation about SMB Direct. Most of the information I read came from the Linux Kernel documentation. All Microsoft says is that it is possible to use SMB Direct on Windows Server with an RDMA enabled interface. SMB itself was actually backwards engineered, but now it appears we have two major implementations of the SMB protocol available in the open source world, `samba` and `ksmbd`. I use both in my network setup, with no issues. Ideally, I'd like to see better interoperability, but I'm writing this in 2024, I doubt this will happen.

SMB direct is also the only easy way to get an RDMA enabled share on Windows. I attempted to do NVMe-oF first. The Linux side is easy, but the Windows side is painful. There are no Infiniband enabled initiators. If you see one, PLEASE reach out to me. Ideally I'd like to go full on block mode remotely, but most of the initiators, including StarWind only support RoCE.

### Reasons for this post

I mainly made this post for the following reasons:

1. I see so much information on forums that is just blatantly incorrect. Confusion of the RDMA protocols, what is possible, and how to implement vary widely.
2. There was no end to end tutorial on this. Even now, after having this setup for at least a year, I see no complete documentation on deploying this type of setup.
3. This particular journey touched numerous high level and low level functionality of multiple operating systems. I thought it would be interesting to write how I approach such a problem.
4. One of my buddies said I never made the post, and now I can tell him to fuck off (in a funny way ofc). This is my spite store.


### Conclusion

I now have to recompile the kernel on AlmaLinux, as I am currently on `6.9RC` with my `ksmbd` setup. Before I expend the cycles to do that, I wanted a reference document in case things go south. This is an informative series of posts, so if anyone actually gets some help from this, please reach out. I would love to hear your story.

Cheers. 👋
