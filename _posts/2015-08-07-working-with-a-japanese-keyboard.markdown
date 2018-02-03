---
author: h0lyalg0rithm
comments: true
date: 2015-08-07 21:24:52+00:00
layout: post
link: http://surajms.com/2015/08/working-with-a-japanese-keyboard/
slug: working-with-a-japanese-keyboard
title: Working with a Japanese keyboard
wordpress_id: 2531
categories:
- Yapp
---

Last week I got a keyboard off of [Souq](http://souq.com) which is a local Amazon competitor.I found a really good deal on it for a genuine apple keyboard for 3 times less the original price.The only gotcha was that the keyboard had both Japanese and English characters on it.It didn't make a lot of difference to me since I was learning some Japanese in my spare time.

The only major issue with the device was the way it was detected on my mac.By default the apple macbook would set the keyboard layout to **international pc  **which worked well with the keyboard but when I didnt use the keyboard the laptop keyboard would get messed up unless I change it back to **US Keyboard. **

My colleague showed me a tool on  the mac called **Keyboard Maestro** which would automate tasks on my laptop like expanding text or sending tasks to omnifocus.<!-- more -->

So this gave me an idea to setup am automatic system which would switch the keyboard layout whenever I would connect the bluetooth keyboard.After some looking around in the settings of Keyboard Maestro I couldn't find an option to set the trigger.

I asked the developers of the software and they were good enough to recommend **ControlPlane**.An open source competitor to them.

ControlPlane works in a more quirky way compared to keyboard maestro, especially the terms they use in the software.



ControlPlane has four important ideas

1)Contexts : Which is similar to profiles on mobile devices.

2)Sources : Sources are like signals which controlplane can support/monitor.

3)Rules : Rules are conditions that you can place on the sources.Like if battery is below 10%.

4)Actions : Actions are actions which are performed it a particular context is set.

To build this automation I had to setup the following.

1)Create two contexts

[![Contexts - ControlPlane](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.13.41-AM.png)](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.13.41-AM.png)

2)Firstly I set bluetooth as the source

[![Sources - ControlPlane](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.11.28-AM.png)](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.11.28-AM.png)

3)I then created two rules for each of the contexts

[![Rules - ControlPlane](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.13.14-AM.png)](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.13.14-AM.png)




[![Rules 1 ControlPlane](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.15.02-AM.png)](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.15.02-AM.png)[![Rules 2 ControlPlanse](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.16.12-AM.png)](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.16.12-AM.png)




4)Finally you have to create two bashscripts which would run tasks on Keyboard Maestro.




The scripts tell applescript which inturn tells keyboard maestro to run a particular task.

5) Now we set the actions based on the contexts in controlplane

[![Actions](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.21.40-AM.png)](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.21.40-AM.png)

[![Actions 2](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.22.13-AM.png)](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.22.13-AM.png)

6) Finally in Keyboard setup two macros : One to change the keyboard to US and the other to International PC.

[![Screen Shot 2015-08-08 at 1.23.50 AM](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.23.50-AM.png)](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.23.50-AM.png) [![Screen Shot 2015-08-08 at 1.23.56 AM](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.23.56-AM.png)](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-08-at-1.23.56-AM.png)

Now you are all setup.Hope this helps
