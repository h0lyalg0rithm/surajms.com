---
author: h0lyalg0rithm
comments: true
date: 2016-01-10 19:11:46+00:00
layout: post
link: http://surajms.com/2016/01/stop-email-tracking-on-gmail/
slug: stop-email-tracking-on-gmail
title: Stop email tracking on Gmail
wordpress_id: 4511
categories:
- Yapp
---

Lately there are many services which track open email, like sidekick from hubspot.The way they work is very straight forward.Any time you open an email sent using sidekick it loads a unique transparent image from sidekick's server thereby letting sidekick know that you have opened the email.This is not a problem if you are using unibox, a mail application that doesn't open images automatically.But Gmail on the other hand loads all the images

Gmail had added a new feature couple of years ago, where it would cache images that are sent in bulk/mass email campaign, making the request anonymous (since google is making the request to the server).However many of these service now generate unique urls for these images.

So the only way to stop the tracking is to stop automatic loading of images.Luckily gmail has the option to disable image loading.![gmail](http://surajms.com/wp-content/uploads/2016/01/gmail-1024x683.png)

To turn off image loading



	
  1. Click on the settings/cog icon on the right hand corner of gmail.

	
  2. Scroll down until you see the images section.Then click on **Ask before displaying external images**.


