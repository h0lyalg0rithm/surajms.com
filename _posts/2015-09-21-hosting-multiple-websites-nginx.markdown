---
author: h0lyalg0rithm
comments: true
date: 2015-09-21 21:05:54+00:00
layout: post
link: http://surajms.com/2015/09/hosting-multiple-websites-nginx/
slug: hosting-multiple-websites-nginx
title: Hosting multiple websites with Nginx
wordpress_id: 176
categories:
- DevOps
---

Nginx is a really awesome web server.It likes a magic tool which does everything you need.

Two weeks I set up a server with multiple websites running on.Since the server was beefy enough we could run 5 websites on it with relatively medium amount of traffic.



The way Nginx allows us to configure multiple websites is using a configuration block in the /etc/nginx/sites-available  or /etc/nginx/sites-enabled directory.Its not necessary to store the configuration in the particular directory but it is treated as good practice.

This is how I setup websites on Nginx.I would first create the configuration file in the **/etc/nginx/sites-available/** directory.Here is the sample configuration.


The most important command to run once you have setup the configuration is **sudo nginx -t.**It doesn't run the server but just tests if the configurations are correct syntactically.

Now that everything is ready, we just have to enable to website configuration.To enable the configuration we create a symbolic link using the following command

    
    ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/example.com


Make sure you include full folder/file path when creating the symbolic link.

To add another website follow the process mentioned above.

Once you are done run sudo service nginx restart.This command will reload the configuration and then restart the server.
