---
author: h0lyalg0rithm
comments: true
date: 2015-02-27 05:01:14+00:00
layout: post
link: http://surajms.com/2015/02/dont-stay-naked-on-an-open-network/
slug: dont-stay-naked-on-an-open-network
title: Don't stay naked on an open network
wordpress_id: 349
categories:
- Chef
- DevOps
- Ruby
---

Everywhere you go either to eat, sleep and even fly.You will always come across open wireless networks.

Currently where I reside most of the shopping malls have free to use Internet.In exchange for your traffic and mobile number you get to access the Internets at crawling speed.These networks are usually open networks, so basically your traffic is naked and unencrypted.Any one can sniff the traffic,inject traffic into your stream and even MITM you, So rather than staying vulnerable target just use a VPN.You have two options to get a VPN,either you buy a VPN from a VPN provider which you cannot certainly cannot trust for anonymity OR the better option setup your own VPN.

Last week I finished my VPN cookbook and this post is a follow up to my previous rant about documentation and how value of open source is diminished without good documentation.

Let's get to the meat of the post,the post will help you setup your own VPN server ,so you no longer have to worry about open networks.



	
  * First you need to get chef installed.Download it from [here](https://downloads.chef.io/chef-dk/).

	
  * Then install two ruby gems to help you install the VPN server.
[Librarian-chef](https://rubygems.org/gems/librarian-chef) a ruby gem to manage your chef repositories.
[Knife-solo](http://matschaffer.github.io/knife-solo/) is like a tool which understand the chef cookbooks and helps you run the code on your server


Once you have the prerequisites installed, create a Cheffile and add my cookbook to it.Your cheffile should look like this.

    
    cookbook 'pptpd', github: 'h0lyalg0rithm/pptpd'


Then run **librarian install** to download all the cookbooks to your computer.

Then run **knife solo user@host** and this will run the chef client on your server and install the recipes.

Once you run it you will notice that it creates a mode directory which will contain a json file.
Edit you json file to add the username and password you want setup in your VPN server.

    
    {
      "run_list": [
        "recipe[pptpd]"
      ],
      "automatic": {
        "ipaddress": "host"
      },
      "pptpd":{
        "users":[{
            "username": "user",
            "password": "password"
          }]
      }
    }


Now you have the VPN setup connect to it.PPTPD is one of the oldest VPN servers out there.It should even work on older smart phones even some of the old nokias.
