---
author: h0lyalg0rithm
comments: true
date: 2015-06-01 18:40:48+00:00
layout: post
link: http://surajms.com/2015/06/gotchas-with-android-studio/
slug: gotchas-with-android-studio
title: Gotchas with android studio
wordpress_id: 1971
categories:
- Android
- Java
- Yapp
---

Android studio is probably the best IDE for Android.Even with its slow grade tasks and occasional unresponsiveness,Google has added a lot of new features to make life easy

Just a couple of days ago I was working with a team to fix an issue they were facing with their android app.

The issue was very vague, the developer was trying to upload a base64 string to the server.The string was generated from an image.But while testing locally on his machine he faced an issue.

I then asked the dev what he was doing ,he said he was using logcat to copy the base64 string.He would then copy the string from the logcat and run it through the online [convertor](http://www.askapache.com/online-tools/base64-image-converter/).

![](http://files.riffsy.com/images/57e9fb2d3d040c1a4215356a354a0328/raw)

So I sat down with the developer to test the code.I put a breakpoint on the string.The debugger showed the obscure string really easy,I then copied the string and pasted it to a online convertor and voila things worked.Although I had to use http://www.miniwebtool.com/remove-spaces/ to remove extra space set by Android Studio.
