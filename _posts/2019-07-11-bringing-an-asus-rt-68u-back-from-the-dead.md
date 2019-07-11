---
layout: post
title: Bringing an Asus RT-68U back from the dead
date: 2019-07-10 16:06 +0200
---

Recently we moved into our new offices, the place is great, large with lots of open space and light.A couple of hours later we started to face some internet issues, my colleagues were not able to connect to the network.I did some digging around and found some Asus RT-68U in the corners of the office.

It seems that my company purchased the equipment left behind by the previous tenant and we continued to use it.
However there was one router which was behaving a bit weird.The LEDs on the device didnt turn on at all but it was still broadcasting a 
wireless signal. My brain jumped to the conclusion that this device was faulty and need a quick reboot.

Several attempts of rebooting, didnt help the device get back to a working state.I then decided to factory reset the device to its original settings and configurations. As instructed by the manufactorer Asus on it's website.I had to hold the reset button for a couple of seconds until the LEDs started blinking.After the first reset, the router stopped broadcasting any wireless network, this made me really worried that the device could have some hardware issue.Even after many resets and restarts, I couldnt get he router working.

I then tried to set the router into firmware restoration mode, a mode where the router would allow me to upload a new firmware onto the device in-order to override the existing one. I was familiar with this mode as its very common in most routers. A standard practice to get to the restoration mode is to perform 30-30-30 reset.A 30-30-30 reset involves pressing the reset button on the router with the power turned off for 30 seconds. While continuing to press the reset button with the power turned on for 30 seconds and finally another 30 seconds with the power turned off.This method usually drains the volatile memory and puts the router into restoration mode.

But this router was not budging.I tried to reset it for 10 minutes, with no luck.Finally before giving up, I thought of trying to reset it with the other buttons on the device.

Her is how I performed the reset in the following order
- Hold the WPS button with router turned off for 15 seconds.
- Connect the device to power
- Continue holding the WPS button for 5 seconds
- Turn off the router why holiding the WPS button
- Press the reset button for 15 seconds
- Turn on the router while pressing the reset button for 5 seconds.
- You will notice the power LED blink rapidly this means the device is now in restoration mode.

I then setup a static IP on my computer's ethernet port.
```
The config
IP: 192.168.1.2
SubnetMask: 255.255.255.0
IP: 192.168.1.1
```

Then all I had to do was connect the device to the computer and visit  [http://192.168.1.1](http://192.168.1.1), I was greeted with a restoration screen and button to upload the new firmware.I uploaded the latest firmware and voila the device ws brought back from the dead.




