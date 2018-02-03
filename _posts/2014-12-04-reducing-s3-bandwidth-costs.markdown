---
author: h0lyalg0rithm
comments: true
date: 2014-12-04 18:50:13+00:00
layout: post
link: http://surajms.com/2014/12/reducing-s3-bandwidth-costs/
slug: reducing-s3-bandwidth-costs
title: Reducing S3 bandwidth costs
wordpress_id: 196
categories:
- DevOps
- Docker
- Haproxy
---

S3 is a good platform to save files without having to worry about storage ,connections and bandwidth.

S3 works on the idea of having buckets of content.The content of the bucket can be private or public or even access control managed.Even if you have a small amounting traffic on your website and the access patterns are every sparse the cost of S3 is low,Moreover Amazon gives about 5gb free every month.But once you reach a scale where you transfer 100 of gigabytes every month the cost per gigabyte for Amazon turns out very high.

Since I was part of a startup with very little cash to spare I came up with this an idea to save bandwidth without having to change the backend or migrate to another provider.The gist of the idea was to set up a reverse proxy server in front of the Amazon servers so every request gets to our proxy server first.Our proxy server in turns makes calls to the Amazon server to get the relevant files.Since a single server cannot handle a bunch load of requests, we also set up a load balancer which distributes requests based on the source ip address.

First we start by creating our amazon cache server.Here is the docker file for it.
{% raw %}
<script src="https://gist.github.com/h0lyalg0rithm/17362c3924d735afbce1.js?file=Dockerfile"></script>
{% endraw %}


The dockerfile creates the nginx servers which proxies traffic from s3.To build the docker image run 'docker build -t s3cache .'

{% raw %}
<script src="https://gist.github.com/h0lyalg0rithm/17362c3924d735afbce1.js?file=default.conf"></script>
{% endraw %}


This config file sets up the reverse proxy and cache configuration for the nginx server.Make sure you replace bucket with your bucket name.This configuration is only applicable to public buckets without authentication.

Lastly we setup the haproxy server.


    docker pull dockerfile/haproxy



You will also have to change the `server ip` to the nginx ip address.To get the ip address of a container run the following command


    docker inspect -f "{{.NetworkSettings.IPAddress}}" <container id>




Once you get the **ipaddress** replace the `server ip` with it and run the following.This will run the docker image.


    docker run -d -p 80:80 -p 8080:8080 -v &lt;dir&gt;:/haproxy-override dockerfile/haproxy




Replace **dir** with the directory that contains the haproxy.cfg file.
To check the status of your haproxy server visit this link
http://dockerip:8080/haproxy?stats
The username is admin and the password is password
Try making some requests you will notice that the requests will always go through the same server due to your ip address.
