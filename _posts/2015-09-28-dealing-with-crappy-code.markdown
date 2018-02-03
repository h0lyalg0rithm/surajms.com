---
author: h0lyalg0rithm
comments: true
date: 2015-09-28 23:00:06+00:00
layout: post
link: http://surajms.com/2015/09/dealing-with-crappy-code/
slug: dealing-with-crappy-code
title: Dealing with crappy php code
wordpress_id: 3541
categories:
- PHP
- Web
- Yapp
post_format:
- Image
---

Last night my friend wanted help with custom PHP cms which he was built for his client.The code was really a mess.You would not know where the code actually began and there was clearly no separation between the model and the views.

I didn't want to spend considerable amount of time in understanding the code.I started debugging the code using the **die **function.Yeah 'die php die'.

die() is a pretty awesome function it is similar to the raising an exception but instead of causing a crash it  just stops code execution for the consecutive lines.You can also pass arguments to the die function.

I was really not sure how the user session was stored/created.So i used the die function by passing the **var_dump($_SESSION)** as the argument, this returns the all the session information.

The php array was returned with a bunch of keys which didn't make sense at all.

The good part about the whole experience was I spent less than 2 minutes in the ugly PHP land.
