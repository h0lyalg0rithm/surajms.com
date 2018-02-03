---
author: h0lyalg0rithm
comments: true
date: 2015-02-23 05:13:59+00:00
layout: post
link: http://surajms.com/2015/02/why-open-source/
slug: why-open-source
title: Why documentation
wordpress_id: 352
---

A couple of months ago I worked on a chef recipe to deploy pptd on your server and I used it to setup my own pptpd  server on host1plus.
I even made it open source on [github](http://github.com/h0lyalg0rithm).last week I had to setup another pptpd server,So this was the right time to reuse the recipe I wrote.It had been more than a month that I had used chef and knife solo to setup the server.

I tried out my recipe and shot things were not working.there were multiple issues with the recipe.the documentation as good as no documentation.i had to go through the ruby code to actually understand the parameters.moreover I had to restart my server to get the iptables rules to apply and on top of it the iptable rules in my recipe were not complete.basically The server would receive data from the client but it would not forward the data to the interface connected to the network.

So with all of this chaos the lesson I learnt was open source is good.open source is not just about writing code,the only way you can make open source work is by supplementing your code with documentation and tutorials which would help others or the future you to get started with using your project.
