---
author: h0lyalg0rithm
comments: true
date: 2015-02-28 14:52:50+00:00
layout: post
link: http://surajms.com/2015/02/fixing-bluetooth-issues-on-yosemite-10-10-2/
slug: fixing-bluetooth-issues-on-yosemite-10-10-2
title: Fixing Bluetooth issues on yosemite 10.10.2
wordpress_id: 363
categories:
- Mac
post_format:
- Aside
---

Lately I have been having issues with my macbook 13in retina 2013.The bluetooth on the mac doesnt connect to any device.After trying a lot of things this is the only solution that worked for me.

    
    sudo launchctl unload /System/Library/LaunchDaemons/com.apple.blued.plist
    sudo launchctl load /System/Library/LaunchDaemons/com.apple.blued.plist


I guess this turns off the bluetooth device deamon/agent and voila bluetooth now works.
