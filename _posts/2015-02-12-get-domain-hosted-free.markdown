---
author: h0lyalg0rithm
comments: true
date: 2015-02-12 16:55:10+00:00
layout: post
link: http://surajms.com/2015/02/get-domain-hosted-free/
slug: get-domain-hosted-free
title: Get your domain hosted for free
wordpress_id: 317
categories:
- Web
---

Hosting a website is pretty cheap nowadays,with most of the hosting websites charging anything from 4$ to 20$ for a small traffic domain.

Recently I came across cloudflare.com CDN service through [mazyod](http://mazyod.com).Cloudflare is a ddos protection service that works by modifying your DNS entries.the best part is that they are free for small websites.

So using Cloudflare and heroku we can get a website running for free with free SSL again (thanks to cloudflare).

To setup your free website


##### Create an account on heroku.com and host your content on it.




##### ![heroku](/wp-contents/uploads/2015/02/heroku.png)




##### Next sign up for their new relic monitoring service though heroku.[Link](https://addons.heroku.com/newrelic)




[![new relic](/wp-contents/uploads/2015/02/new-relic-902x1024.png)](/wp-contents/uploads/2015/02/new-relic.png)
One gotcha about heroku is that it puts your app to sleep if it doesn't receive any traffic for a particular amount of time.New relic offers a service where they check the status of the website after a particular interval of time.This check forces your app on heroku to stay away preventing from sleeping.




To activate this service go to application monitoring in the new relic dashboard and enter your **domain url **




[![newrelic_ping](/wp-contents/uploads/2015/02/newrelic_ping-1024x869.jpg)](/wp-contents/uploads/2015/02/newrelic_ping.jpg)
Next setup the Cloudflare account and point your nameserver to cloudflare.To use cloudflare set your nameserver to **mary.ns.cloudflare.com **or** tim.ns.cloudflare.com**




Once you are done, create a **CNAME** record in cloudflare with value of YOUR_HEROKU_APP_NAME.herokuapp.com.




You can check for this value in your heroku settings.




![heroku_settings](/wp-contents/uploads/2015/02/heroku_settings-1024x794.jpg)



