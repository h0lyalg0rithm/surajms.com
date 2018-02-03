---
author: h0lyalg0rithm
comments: true
date: 2015-08-16 17:49:24+00:00
layout: post
link: http://surajms.com/2015/08/update-gemfile-with-ease/
slug: update-gemfile-with-ease
title: Update Gemfile with ease
wordpress_id: 2821
categories:
- Ruby
---

Yesterday I came across this nifty tool to update the version numbers in my Gemfile.

[![Gemfly](http://surajms.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-17-at-9.51.19-PM-1024x786.png)](http://gemfly.findings.co/)

Now you might be wondering why not just use the bundler to take care of stuff.The problem with bundler is firstly its slow and whenever there are transient dependencies it would tell us to update the dependency rather than taking care of it.
 
Take a look at it [Gemfly](http://gemfly.findings.co/)
