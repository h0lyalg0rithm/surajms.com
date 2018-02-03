---
author: h0lyalg0rithm
comments: true
date: 2015-11-11 15:13:27+00:00
layout: post
link: http://surajms.com/2015/11/easy-captive-portal-with-nodogsplash/
slug: easy-captive-portal-with-nodogsplash
title: Easy captive portal with nodogsplash
wordpress_id: 3971
categories:
- Hardware
---

For the last 2 weeks I was busy with a hardware startup called [MyTriphoto](http://www.mytriphoto.com/).The whole premise of the startup is to take panoramic selfie without touching the camera.To accomplish this we have been working on a hardware prototype built using the raspberrypi and a 360 camera.The user connects to the wireless network setup by the raspberrypi and the router. The user is then greeted with the webapp on this phone.

So to get this working I had to setup a captive portal on the the router.I looked around for existing solutions and came across nocatsplash.After digging a bit more I found nodogsplash.NoDogSplash is based off of nocatsplash with a bunch of new features and easier configuration manager.

To setup nodogsplash on MR3020 was a breeze.
All I had to do was update the package repositories and install nodogsplash.
Here is how i installed it.

    
    opkg update
    opkg install nodogsplash


Time to configure the portal.Luckily the documentation for nodogsplash was really good.The configuration was heavily commented and with a bunch of configuration options.
