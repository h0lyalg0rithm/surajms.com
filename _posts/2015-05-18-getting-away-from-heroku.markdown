---
author: h0lyalg0rithm
comments: true
date: 2015-05-18 20:54:50+00:00
layout: post
link: http://surajms.com/2015/05/getting-away-from-heroku/
slug: getting-away-from-heroku
title: Getting away from heroku
wordpress_id: 315
categories:
- DevOps
---

Heroku is a really cool service.It lets me snip up servers in a matter of minutes rather than hours.But Heroku has a dark side, as a developer heroku provides you a free instance which should be sufficient for your regular testing and development process.But as soon as you want to launch your application, you will get deterred by the amount of money you will be paying per month

Starting from my last project I have been trying to move away from heroku and build the features that heroku offers.The process would look something like this.



	
  1. Automatic deployment and running of Tasks (Done)(Thanks to capistrano)

	
  2. Auto Scaling of website based on CPU usage.

	
  3. Deployment of code once the test pass.




### 1.Automatic deployment and running of Tasks


Capistrano plays a huge role in the this step,I was able to deploy the code from my machine without even touching the server.No more ssh and managing different deployment version.


### 2.AutoScaling of website


This is probably the most difficult part of the whole setup.AutoScaling in the cloud world is very dependent on the service provider you chose.Microsoft Azure , Amazon AWS and DigitalOcean all have a different way to launch and provision website.Currently I have got the server provisioning working but integrating the code deployment and load balancer is still very tedious.


### 3.Deployment of code once the test pass


This step of the process will also rely on a tool which is mostly gonna be jenkins.Jenkins is very popular and it has huge community of existing plugins which I can make use of.


