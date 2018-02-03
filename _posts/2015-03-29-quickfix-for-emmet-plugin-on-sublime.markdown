---
author: h0lyalg0rithm
comments: true
date: 2015-03-29 17:44:21+00:00
layout: post
link: http://surajms.com/2015/03/quickfix-for-emmet-plugin-on-sublime/
slug: quickfix-for-emmet-plugin-on-sublime
title: QuickFix for emmet plugin on sublime
wordpress_id: 376
categories:
- Mac
- Web
---

[Emmet](http://emmet.io/) has a really awesome plugin for sublime text.The plugin depends on PyV8 to function.But by default the plugin tries to download the latest version of the plugin from the internet.This is all well until you have a stable internet connection.Since PyV8 is not updated frequently you can download the binary locally for sublime to use.

This are the instructions I followed to get the plugin to work offline.



	
  * First download pyv8 binary for you operating system from [here](https://github.com/emmetio/pyv8-binaries).

	
  * Then click on Sublime > Preferences > browse package.This will open the file explorer/Finder.

	
  * Create a directory in the Packages folder called **PyV8.**Extract the binary into that folder.Example(PyV8/osx-p3) osx for the operating system.

	
  * In the osx-p3 directory you will find a config.json file.Open the file in sublime and change _skip_update_ from false to **true**.

	
  * Now its time to edit the emmet config file.Click on Sublime > Preferences > Package Settings > Emmet > Settings - User.Add the following line to it '{"disable_pyv8_update": true}'.


Now you can use sublime with emmet.io offline without needing to download PyV8 every-time on launch.


