---
author: h0lyalg0rithm
comments: true
date: 2015-05-14 10:19:20+00:00
layout: post
link: http://surajms.com/2015/05/integrating-clockwork-with-capistrano/
slug: integrating-clockwork-with-capistrano
title: Integrating clockwork with capistrano
wordpress_id: 1621
categories:
- Ruby
---

Today I am write about a gem that I released a couple of days ago.The gem allows you to integrate the clockwork gem with Capistrano.
Capistrano is a really powerful tool to automate deployment and perform tasks during or after the deployment.

Clockwork is the cron job of Ruby world.Compared to the whenever gem (another cron gem) clockwork much more expressive and its looks very rubyish.

I looked around for a a plugin for Capistrano which would help me restart clockwork whenever I would deploy.

Using Capistrano-clockwork is very straightforward, like most the Capistrano plugins,it only supports capistrano 3 and above.
All you have to do it mention Capistrano-clockwork in your gemfile and add 'capistrano/clockwork'

That's it.from now onwards whenever you deploy the gem restarts clockwork

If you don't want the clockwork daemon to restart ,you can disable it by setting clockwork_default_hooks to false

    
    set :clockwork_default_hooks, false


Moreover you can perform other tasks via the following commands:

    
    cap clockwork:start
    cap clockwork:restart
    cap clockwork:status
    cap clockwork:stop
