---
layout: post
title: Autoupdate bricked my phone
date: 2024-02-02 17:22 +0100
---
Starting from this year I decided not to spend time building and running my own infrastructure.
Until the end of Jan 2023 I would always build the rom from scratch rather than depending on the maintainer to release a new build of the rom.

Today morning I allowed my phone to be updated to the latest build of ArrowOS, what I didnt know was that it was an automatic monthly build.This ended up bricking my phone.

![My phone is dead](/wp-contents/uploads/2024/02/phone_dead.gif)

My first action was trying to revert it back to an older build.Checking the ArrowOS download website for previous builds, resulted in nothing.Looks like older build links were removed from the website. I checked my machine for an older build and I found one however do the mismatch in the security patch level prevented recovery from sideloading the older build.

Looking on the telegram group, I didnt see much activity from the maintainer. I decided to pull up my sleeves and built the rom from scratch.
This time I setup a machine on [clouding.io](https://clouding.io), they are a local(Spain) cloud hosting service which is fairly priced.The best part about them is that they have fast NVMe disks, must have for building roms and their snapshot pricing is much lower than others even 5-10x cheaper than the big guys like Google, DigitalOcean etc.

I ended up building the rom, I removed the offending commit which resulted in the issue.Seems like those commits did not have any side-effects as I am running the rom now without any issues.

