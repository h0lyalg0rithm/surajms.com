---
author: h0lyalg0rithm
comments: true
date: 2014-12-03 08:51:31+00:00
layout: post
link: http://surajms.com/2014/12/monthly-docker-cleanup/
slug: monthly-docker-cleanup
title: Monthly docker cleanup
wordpress_id: 197
categories:
- DevOps
- Docker
---

Getting rid of docker containers can be a pain.Its been about 6 months I have been using docker to build images for development purposes.
I took at my free space and I have only a couple of gigs free (5 gigs to be exact).It was time to clean this shit up.

    
    docker rm $(docker ps -a -q)
    #This removes all docker containers which have exited
    
    docker rmi $(docker images -q)
    #This deletes all the docker images.



