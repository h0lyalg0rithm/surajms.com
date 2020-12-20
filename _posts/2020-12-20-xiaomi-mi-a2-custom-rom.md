---
layout: post
title: Xiaomi Mi A2 custom rom
date: 2020-12-20 22:17 +0100
---
Recently I updated my phone from a Xiaomi Mi A2 to a Pixel 2 XL.Even though Mi A2 runs android one, Google/Xiaomi no longer will update the device to the latest version of the OS.Moreover the rom development community is large and thriving with multiple stable versions of Android 11 roms for the device.
This makes the Mi A2 and ideal device for testing and playing around.

Installing custom roms on any android device involves the following steps:
- Unlocking bootloader
- Installing PBRP
- Installing the rom

### Unlocking the bootloader
This is usually the most complicated bit of the whole process.Usually for non-Pixel devices the process involves getting some special unlock code from the manufacturer, however Mi A2 was based off Android one so Google makes its pretty easy to unlock the bootloader.

I had already enable debugging mode and OEM unlocking option by unlocking the developer options.This involves pressing the android build number 5 times in the about page.
```
adb reboot bootloader
fastboot oem unlock
fastboot flashing unlock_critical
```
The steps above would clear out the device and run the factory reset procedure.

### Installing PBRP
Installing PBRP allows us to test out different custom roms with a safety net.I downloaded the latest twrp img from the [xda forum](https://forum.xda-developers.com/t/official-recovery-pitchblackrecoveryproject-pbrp-for-xiaomi-mi-a2-jasmine.3830864/).It is a custom fork of TWRP with easier UI with lots of bells and whistles.
```
fastboot flash recovery pbrp.img
```
Alternatively you could just boot into PBRP without installing it.
```
fastboot boot recovery pbrp.img
```
### Installing the ROM
Instead of downloading the rom directly from the [ArrowOS](https://arrowos.net/) website.I built the image from source to understand the build process.I will make another post on this process.For now we can use the prebuilt image and install it on the device.I push the rom to the device using the following command
```
adb push rom.zip /data/media/0
```
I then switch the active partition to slot A so that the rom is installed on slot B.The partition slots is a new feature introduced in Android 9 and above which allows us to run multiple versions of android on the same device.This is something I will try next.

Using the PBRP UI I installed the rom using the install button in the recovery ui.

And voila the rom is installed and the phone is ready with the new version of Android.
