---
title: "Neetcode 7/150 - Product of Array Except Self"
date: 2024-08-06T17:09:01-04:00
---

### Intro

This is entry `7/150` in the NeetCode150 Challenge.

The associated video is here: 

[Software Development | Neetcode 7/150 - Product of Array Except Self](https://youtu.be/7iZ7JwjMGT8)

### Problem

The problem states:

> Given an integer array `nums`, return an array answer such that `answer[i]` is equal to the product of all the elements of nums except `nums[i]`.
> 
> The product of any prefix or suffix of `nums` is guaranteed to fit in a 32-bit integer.
> 
> You must write an algorithm that runs in `O(n)` time and without using the division operation.

### Root Cause Analysis

After watching my performance on this recording, it is clear that I am getting the naive solution fairly quickly. We need to just multiply all numbers, other than the current positional element, and store those results. Simple right?

*TLE* 

Hmmmm ... what went wrong? I had someone in chat tell me that I needed to code `O(n)` solution but this actually didn't help, since the problem clearly states that. At this point I'm asking myself:

> How is it possible to calculate products with one pass of the array?

The trick to this problem is utilizing a prefix/postfix sum approach. Prior to this problem, I had never even heard of this approach. Honestly, they probably went over it one day when I skipped my algorithms class (sorry Prof. Assadi). Regardless, this a neat way to treat subarray problems.

After viewing my video, I was surprised I didn't think about using a sliding window technique. Apparently this approach doesn't work for this problem. Therefore, I need to be able to identify when to use each of these methods.

Either way, subarray type problems appear to come up quite frequently (substrings as well). I need to start compiling the commonly used algorithms for each ADT. This brings us to the actual reason for failure.

### Summary

I failed this module due to the following reasons:

1. Not knowing prefix/postfix methods of evaluating subarrays.
2. Not having a clear algorithm and optimization method to even begin experimenting with.
3. Coding the naive method and wasting time.


### Action items

1. Gather different strats for the Array/Hashmaps data types.
2. Get an algorithm on paper first before coding.
3. Do not code the naive solution.

### Final thoughts

I've now done seven of these. I have written my thoughts on how I can improve and intend to do so. One of these is a reflection post after each Neetcode section. My record is terrible. I need to improve. All future posts will follow this format. It is just easier for analysis to have it broken down like this.

### Stream info

I stream these Neetcode problems on Twitch and have the recordings on YouTube. You can watch me attempt this module or follow me on any of the links below.

👇

[Twitch](https://twitch.tv/Mexpat911)

[YouTube](https://www.youtube.com/@mexpat911)
