---
author: h0lyalg0rithm
comments: true
date: 2014-08-23 16:45:18+00:00
layout: post
link: http://surajms.com/2014/08/quick-debugging-web-console/
slug: quick-debugging-web-console
title: Quick debugging with web-console
wordpress_id: 149
categories:
- Rails
- Ruby
---

![error](http://surajms.azurewebsites.net/wp-content/uploads/2014/08/error-1024x734.png)
Most of us have seen this dreaded error page when developing on rails.Launching up irb or rails console wastes a lot of time and brain cycles.
Having said that I came across this neat gem called 'web-console'.This gem is really handy ,it launches rails console right there is the browser along with the current context.
Installing it is pretty simple Add it to your Gemfile and you are up and running.Make sure you have the version mentioned below or something higher.

    
    gem 'web-console', '2.0.0.beta2'


![web-console](http://surajms.azurewebsites.net/wp-content/uploads/2014/08/web-console.png)
