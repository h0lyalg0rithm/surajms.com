---
author: h0lyalg0rithm
comments: true
date: 2014-03-09 12:32:48+00:00
layout: post
link: http://surajms.com/2014/03/apache-server-on-docker/
slug: apache-server-on-docker
title: Apache server on docker
wordpress_id: 40
categories:
- Docker
---

Docker is a light weight virtualization tool which uses the lxc(linux containers) to run its virtual machines.
Docker uses dockerfile to create the virtual machines.To setup the apache server with php on docker is very simple.
We first create a Dockerfile with the following command

    
    touch Dockerfile 


This creates an empty file.Lets first get the base ubuntu  files for the vm.
    
    docker get ubuntu

.This will pull the ubuntu files form docker's servers.Now we need to add the some commands to the dockerfile for docker to run.

    
    
    FROM ubuntu
    MAINTAINER Suraj Shirvankar
    


This instructs docker to use the ubnutu base files and also set suraj as the maintainer of the dockerfile.
We then run apt-get update  which fetches the package info using aptitude.We also run the apt-get install apache2 to install the apache2 server.

    
    
    FROM ubuntu
    MAINTAINER Suraj Shirvankar
    RUN apt-get update
    RUN apt-get install apache2 -y
    


Since we will be using php with apache we install the php.We will also need the libapache2 module for php to work with apache2.

    
    
    FROM ubuntu
    MAINTAINER Suraj Shirvankar
    RUN apt-get update
    RUN apt-get install apache2 -y
    RUN apt-get install php5 libapache2-mod-php5 -y
    



Now that php and apache is available we can start the apache2 service.

    
    
    FROM ubuntu
    MAINTAINER Suraj Shirvankar
    RUN apt-get update
    RUN apt-get install apache2 -y
    RUN apt-get install php5 libapache2-mod-php5 -y
    RUN /etc/init.d/apache2 start
    CMD /bin/bash
    



Finally you run the docker build program.

    
    
    docker build -t apache2 .
    
