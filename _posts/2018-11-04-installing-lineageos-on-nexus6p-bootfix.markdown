---
author: h0lyalg0rithm
comments: true
date: 2018-11-04 02:17:14+01:00
layout: post
link: http://surajms.com/2018/11/install-lineageos-on-nexus6p-bootfix/
slug: install-lineageos-on-nexus6p-bootfix
title: Install Lineage OS on Nexus 6P with bootfix
categories:
- Random
---

Since the middle of this year I switched my phone from a Nexus 6P to a Pixel 2.The switch was definitely a good decision as my ill-fated Nexus 6P had a hardware issue resulting in [Bootloop of Death](https://forum.xda-developers.com/nexus-6p/general/bootloop-death-blod-workaround-zip-t3819515).Common issue with most of the Nexus devices, Damn you Huawei.

Physically the phone was in a good condition, it worked very well until it died on me.After searching online for some solution, i could conclude that the issue was with the SOC.The high power CPU was defective and the only way to make the device work was to disable the heavy duty CPU.

As it had been more than 8 months since I used the device, the first thing I tried to do was install the latest version of android, however it failed as the OTA would enable the high power cpu.

To make things interesting, I decided to use Lineage OS without Google's services.Lineage OS just like the OTAs would try to use all of the CPUs on the phone resulting in the BLOD.

Looking around I found a fix and here are the steps I had to follow in order to make it my phone work.

Requirements:
1. Mac
2. Decent Internet (Lineage OS images are large)

Actions:
1. Download and extract the latest version of Lineage OS from [Lineage OS download](https://download.lineageos.org/angler)
2. I downloaded and extracted Android Image Kitchen for Linux from [https://forum.xda-developers.com/showthread.php?t=2073775](https://forum.xda-developers.com/showthread.php?t=2073775)
or [https://github.com/osm0sis/Android-Image-Kitchen/tree/AIK-Linux](https://github.com/osm0sis/Android-Image-Kitchen/tree/AIK-Linux)
3. In the terminal, run `unpackimg lineageos/boot.img`.This will extract the boot.img into the ramdisk and split_img folders.
4. Here comes the important parts.We need to set the total number of CPUs to 4(efficient cores)
Around line 85(Might be different for newer versions)  
Edit `init.angler.rc` in the ramdisk directory    
```
 write /dev/cpuset/foreground/cpus 0-3
 write /dev/cpuset/foreground/boost/cpus 0-3
 write /dev/cpuset/background/cpus 0
 write /dev/cpuset/system-background/cpus 0-2
 write /dev/cpuset/top-app/cpus 0-3
 write /dev/cpuset/camera-daemon/cpus 0-3
```
5. Edit the `boot-img.cmdline` in the split_img directory  
  Add `maxcpus=4` to the end of the first line.
6. Then run `repackimg.sh` to build the new boot.img file.
7. Here comes the tricky bit, since the zip extractor on mac does understand the directory structure we should use an application like [ZipCreator](http://zipcreator.com).Its a java application that will allow you to replace files inside an existing zip file.Now replace the old `boot.img` from the original lineage OS zip file with the one generated in the Android Image Kitchen directory.
7. Save and flash the new image onto the nexus.

I had to perform a couple of extra steps like install a new bootloader however its not mandatory but a good step to take.You can download a pre-patched 4 core fix [TWRP 3.2.1](https://androidfilehost.com/?fid=745849072291698840) or on this [website](https://forum.xda-developers.com/nexus-6p/general/guide-tutorial-nexus-6p-bootloop-death-t3716330).
Flashing the bootloader was quick
```
adb reboot bootloader
fastboot flash recovery TWRP.img
fastboot reboot
```
I had to install the latest vendor image as well since there was an issue with the lineageos build.  
```
fastboot flash vendor vendor.img
```
