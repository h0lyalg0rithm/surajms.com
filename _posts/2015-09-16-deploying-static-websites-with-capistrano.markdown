---
author: h0lyalg0rithm
comments: true
date: 2015-09-16 19:18:18+00:00
layout: post
link: http://surajms.com/2015/09/deploying-static-websites-with-capistrano/
slug: deploying-static-websites-with-capistrano
title: Deploying static websites with capistrano
wordpress_id: 1591
categories:
- DevOps
- Ruby
- Web
---

In my quest to move away from heroku. I came across Capistrano a popular automated deployment tool written in Ruby. Capistrano is really popular with millions of downloads and lots of Plugins

Here is how I setup Capistrano to deploy static websites and create rollbacks in case the build was buggy.

{% gist 84431cc248454fed8754 %}


Capistrano deploys the code to /var/www/application_name.It does so by logging in the user into the server and pulling the repo from the git repo specified.On top of this capistrano adds a bunch of commands to make this process simpler.

Running

    cap -T

shows the lists of commands capistrano supports.
