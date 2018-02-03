---
author: h0lyalg0rithm
comments: true
date: 2014-06-01 18:10:21+00:00
layout: post
link: http://surajms.com/2014/06/automating-builds-with-jenkins/
slug: automating-builds-with-jenkins
title: Automating builds with jenkins
wordpress_id: 107
categories:
- Jenkins
---

From next week onwards I will be dealing with atleast 7 or more clients who want their app build in 2 months.That roughly gives me about.

    
    var time = 60 days;
    var clients = 7;
    var time_per_project = 60/7 = 8.5 days




So now was the time to get my software development stuff ready things like chef recipes and build system.
Since I had never setup a integration server from scratch,I thought this will take lot of time as the build servers are based on java and my inexperience in the java deployment scene made me even more reluctant.

Once I got over this.I went to the jenkins website to download the java version.I was so worried it would mess up my system.I created a vagrant host.Install java and the other dependencies.But to my surprise It was pretty simple to setup.All i had to do was run

    
    java -jar jenkins.war


Boom and now i have a build server running inside my host.To prepare my build task I had to write a script file which the build server would run and then i would have all the test running.
