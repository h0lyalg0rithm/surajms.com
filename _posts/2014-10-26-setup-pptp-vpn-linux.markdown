---
author: h0lyalg0rithm
comments: true
date: 2014-10-26 06:21:19+00:00
layout: post
link: http://surajms.com/2014/10/setup-pptp-vpn-linux/
slug: setup-pptp-vpn-linux
title: Setup pptp vpn on linux
wordpress_id: 178
categories:
- DevOps
---

For a couple of days I was looking for an extremely cheap vps provider on websites like [lowendtalk](http://www.lowendtalk.com/) .Having a vpn handy is really useful especially when using an network.After going through a lot of the providers and their infrastructure, I landing on [host1plus](http://www.host1plus.com/).

Host1Plus is an extreme cheap VPS provider where the hosting starting from 2$ and goes up depending on the hardware specs you select.For a standard VPS with about 3-4 concurrent users a 256 MB ram computer is sufficient enough.Setting up this vpn was really easy all i had to do was install the pptpd package from the ubuntu repository.After some minor configuration changes I was up and running with a VPN that works and routes all my traffic though it.

The vpn was working fine for a couple of days until one day i could not connect to it.Seems like there was an issue with the host1plus network configuration due to which i was not able to reach my server.So i logged onto the admin dashboard and reinstalled the OS with their oneclick **reinstall** button.I had to go through the same process as before to setup the users , iptables ......

I had been playing around with chef for a couple of months now.So I though making a chef cookbook to install pptp and configure would make the setup really easy.Just running one command with smart default was the primary goal of this cookbook.

So I wrote a cookbook which is available on [github](https://github.com/h0lyalg0rithm/pptp).To use the cookbook you need chef installed.And you need to add the **pptpd** recipe to the _node.json_ file.

Other details on how to use the cookbook is available on [README](https://github.com/h0lyalg0rithm/pptp/blob/master/README.md).

Writing the cookbook was easy given chef has a very clean and neatly defined DSL to perform actions on the server.
