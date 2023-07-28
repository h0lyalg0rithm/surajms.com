---
layout: post
title: Yet another bootloader fail
date: 2023-07-29 01:05 +0200
---
Last week I ended up hard bricking my Pixel 2 XL with a stupid mistake,I ended up locking my bootloader with an invalid partition.This was a hard brick and the only ones who can unlock is google.I tried to schedule a repair through the google store.Their cost estimator returned a cost to repair nearly the price of a new google pixel.
So I decided to switch back to my old Xiaomi A2.I turned on the device after a while and the operating system on the device was more than 3 years old.

I decided to build PixelExperience rom for my device, It took a while as my HDD was pretty slow.However it completed in 2 hours.
This is how I got the rom installed on my device.

- I first booted into the bootloader using adb. `adb reboot bootloader`
- I then flashed the bootloader on both the partitions
```
fastboot --set-active=a
fastboot flash boot recovery.img
fastboot --set-active=b
fastboot flash boot recovery.img
```
- I then  ran `fastboot reboot recovery` to boot into recovery.
- I then had to flash the following [zip](https://github.com/PixelExperience-Devices/blobs/raw/main/copy-partitions-20210323_1922.zip) which sets up the new partition scheme required for newer versions of android, using the adb sideload option in recovery `adb sideload copy-partitions-20210323_1992.zip`
- Next I had to reboot into recovery again using the ui.
- To support dynamic partitions I had to flash the following [img](https://gitlab.pixelexperience.org/android/vendor-blobs/wiki_blobs_jasmine_sprout/-/raw/main/android-13/super_empty.img?inline=false), however the way to flash it is a bit different.
- I had to switch to fastboot using the recovery screen and then run the following `fastboot wipe-super super_empty.img`
- I then performed a factory reset on the phone.
- The active partition was set to `b` so that the inactive partition is `a` where the recovery would install the operating system.
- Once that was complete I had to switch back to recovery and sideload the final rom `adb sideload pixelexperience_jasmine_sprout.zip`
- Another factory reset on the phone just to be safe.
