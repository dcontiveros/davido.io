---
title: "Live"
date: 2023-01-10T12:29:02-05:00
---

I have ensured that the new version of the site is now accessible and serving https via Let's Encrypt certificates.

A few things about Let's Encrypt. I don't really mind the constant refreshing of the SSL cert. I do have a cron job that is dedicated to this. However, I am not using certbot. I have found [acme.sh](https://github.com/acmesh-official/acme.sh) suits my needs better and is pure shell.

Call me a purist. Things are going well so far with this deployment. We'll see what happens when it comes time for upgrades.
