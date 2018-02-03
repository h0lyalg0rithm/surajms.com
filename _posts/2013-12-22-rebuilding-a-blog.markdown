---
author: h0lyalg0rithm
comments: true
date: 2013-12-22 08:30:57+00:00
layout: post
link: http://surajms.com/2013/12/rebuilding-a-blog/
slug: rebuilding-a-blog
title: Rebuilding a blog
wordpress_id: 1
---

After destroying my previous blog(thanks to ec2).I have planned to take regular backups of my blog.Making sure I have a hot as well as soft backup,everything from the theme i developed to the content on the page.

Steps I have taken to prevent such a mishap.



	
  * Version Control - I am starting to version control the theme I will use on the site .

	
  * Remote repository - Having a remote repository is useful as it works as a backup with the added benefit of working remotely.I am using Bitbucket ([link](http://bitbucket.org)) which allows me to have unlimited private repositories and it is completely free.

	
  * The server deployment itself is version control as I have installed it with chef([link](http://opscode.com/)).

	
  * Lastly I have installed Backwpup which is a free plugin for wordpress.I does automatic backup of the data similar to a cron job.It lets you make a complete backup of you database as well as the wp-content folder of the website.



