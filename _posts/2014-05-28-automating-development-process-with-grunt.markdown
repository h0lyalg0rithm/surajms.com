---
author: h0lyalg0rithm
comments: true
date: 2014-05-28 05:52:30+00:00
layout: post
link: http://surajms.com/2014/05/automating-development-process-with-grunt/
slug: automating-development-process-with-grunt
title: Automating development process with grunt
wordpress_id: 103
categories:
- Grunt
- Javascript
---

Grunt is an awesome javascript tool to automate your build process.The best part about gruntjs is how quickly you can build tasks.I came across this [project](https://github.com/leemunroe/grunt-email-design) which lets me build html email templates which work well with most browser.

The most important feature of this project is that it automatically builds and inlines the css.Emails need to have inline css because all of the email client in existence do not allow external stylesheets especially outlook.

This project is great once you create an email template you have it sent to your inbox to test.It also supports cloudfront cdn to have your email attachments in the cloud.

I am a big fan of mailchimp and their email service,I wanted to mailchimp's smtp server to send the email to me rather than the built in mailgun(Mailgun is awesome too).I looked around for a grunt plugin for mailchimp.After a couple of minutes searching,I decided to write my own grunt plugin to send the email.

Since mailchimp calls it's email service mandrill.I did the logical thing and named the plugin grunt-mandrill(I suck at naming things)

The plugin is pretty simple.You add the configs in your Gruntfile and add the grunt-mandrill task to it.

Back to grunt-email-design.
I have integrated the plugin with the email design repo,pull request is still pending.But if you want to use mandrill head over to my [github repo](https://github.com/h0lyalg0rithm/grunt-mandrill)  to use it.
