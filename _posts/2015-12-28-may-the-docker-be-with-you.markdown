---
author: h0lyalg0rithm
comments: true
date: 2015-12-28 19:59:01+00:00
layout: post
link: http://surajms.com/2015/12/may-the-docker-be-with-you/
slug: may-the-docker-be-with-you
title: May the docker be with you
wordpress_id: 4371
---

2015 was year of docker.I too was very skeptical of using docker for production.But coming to the end of the year, my views have changed on it drastically.This change was mostly due to the improvements in the developer workflow and maturation of tools like docker-compose(Formerly fig).

My three major concerns with docker were



	
  * How do I store persistent data essential in cases like running a database or image datastore.

	
  * Deployment of containers.

	
  * Running development environment like guard which listens for file changes and runs tasks like tests / code linting.


The first two of my concerns were resolved, but the last one still lingers.This issue is mostly due to the way docker is setup,during development I run docker using boot2docker since I work on a mac.Guard is a really essential tool while developing rails backends.Since it runs your tests whenever your code changes.This provides rapid feedback and helps to get into the RED GREEN RED code flow.However docker doesnt push the file changes trigger back to guard,rendering it useless.

I would like to end this post on a high note.The Docker community is growing and there are lot of changes to come to docker.
