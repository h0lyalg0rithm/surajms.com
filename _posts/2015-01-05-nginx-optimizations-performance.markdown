---
author: h0lyalg0rithm
comments: true
date: 2015-01-05 14:23:28+00:00
layout: post
link: http://surajms.com/2015/01/nginx-optimizations-performance/
slug: nginx-optimizations-performance
title: Nginx optimizations for performance
wordpress_id: 238
categories:
- Nginx
---

Nginx is a really powerful server with lots of room for customisation.Just a couple of days ago I worked on a website which delivered a lot of assets to the browsers and performance was of utmost important for the client.

Nginx stores its configuration file in the /etc/nginx/nginx.conf file.

    
    location ~* .html$ {
    	expires 3d;
    }
    location ~* .(mp4|mp3|ttf|css|rss|atom|js|jpg|jpeg|gif|ogg|ogv|svg|svgz|eot|otf|woff|png|ico|zip|tgz|gz|rar)(?ver=[0-9.]+)?$ {
    	access_log off; 
    	log_not_found off; 
    	expires max;
    }


Since the assets dont change we set the Cache-Control to max time.

For html pages we let it expire every 3 days.Since its updated regularly.

    
            gzip on;
            gzip_disable "msie6";
    
            gzip_vary on;
            gzip_proxied any;
            gzip_comp_level 6;
            gzip_buffers 16 8k;
            gzip_http_version 1.1;
            gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;
    




**gzip on -** This is probably the simplest of all.It just turns on the GZIP module which is part of nginx.

**gzip_disable "msie6" -** Since IE 6 doesnt support gzip we disable sending gzip in the header of the response.

**gzip_vary on -** Many proxies/cdns require this option so it can serve both the compressed and non compressed version of the content.More info at [maxcdn](https://www.maxcdn.com/blog/accept-encoding-its-vary-important/)

**gzip_proxied any -** It enables gzip on all proxy requests.
**gzip_comp_level 6 - ** This sets the compression level.Level 6 is a sweet spot as the value ranges from 1 to 9.Higher the compression more cpu cycles will be eaten.
**gzip_buffers 16 8k - ** Not really sure.I think they are default values.
**gzip_http_version 1.1 - ** Mininum http version to be supported by the browsers.
**gzip_types -** Enable gzip for the following files.
