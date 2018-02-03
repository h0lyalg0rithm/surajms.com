---
author: h0lyalg0rithm
comments: true
date: 2014-05-18 17:12:17+00:00
layout: post
link: http://surajms.com/2014/05/whats-new-rails-4-1-2/
slug: whats-new-rails-4-1-2
title: Whats new in Rails 4.1
wordpress_id: 92
categories:
- Rails
---

Continuing with previous [post](/whats-new-in-rails-4-0/),this post will cover whats new in Rails 4.1 .
Most of my information comes from the blog post on the rails [blog](http://edgeguides.rubyonrails.org/4_1_release_notes.html).This is my take on the new features and will mostly cover the ones useful for me in my day to day development.

To speed up our development start time and test ,rails preloader has now been replaced with spring, which works just like spork.It creates a separate process which loads the rails environment in memory thereby reducing time for running our test as rake reloads the rails environment every time we run a rake task.

I have been using the env gem to store my secret_keys for apis like facebook,aws..etc.Rails now has the secrets.yml in the config folder.We can now store all the configuration keys in the secret.yml file.We can retrieve the key using the Rails.application.secrets.{secret_name}.

ActiveRecord Enums is another important feature.Even though it is something trivial to implement.Rails makes it easier to store stat of a particular model to a particular integer.Plus it creates many handy methods which is provides to query.



There are many more changes ,to learn about them visit this [link](http://edgeguides.rubyonrails.org/4_1_release_notes.html).


