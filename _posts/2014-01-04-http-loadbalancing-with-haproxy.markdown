---
author: h0lyalg0rithm
comments: true
date: 2014-01-04 13:40:13+00:00
layout: post
link: http://surajms.com/2014/01/http-loadbalancing-with-haproxy/
slug: http-loadbalancing-with-haproxy
title: HTTP loadbalancing with haproxy
wordpress_id: 20
categories:
- Haproxy
tags:
- Haproxy
---

If you are planning to scale your website to accommodate for extra traffic on the website.You have two options you can scale vertically or horizontally.
Vertical scaling usually involves adding extra ram/processing power which may be desired,but there is a limit to this kind of scaling.
Horizontal scaling is were you setup multiple machines and they work together to get the work done.Haproxy is loadbalancer which will let you scale your infrastructure horizontally.

To setup loadbalancing between 2 machines is pretty simple.Firstly you will require two machines with static address or a DNS entry to identify the machines.

I will using vagrant during this process of setting up a loadbalancer.I will be using vagrant a virtual machine environment which does have a gui.More information about it can be found at http://vagrantup.com/.

I have setup up virtual machines running ubuntu 13.04 LTS.Both the machines are running Apache2 with default settings.You can replicate the same by running this on the terminal.

    
    
    sudo apt-get update
    sudo apt-get install apache2 php5
    sudo apt-get install libapache2-mod-php5
    sudo service apache2 restart
    



Next we get the ip address of the two machines and store them someplace safely.

    
    
    ifconfig eth0
    


The ip address of machine one is 10.0.2.2 and the second machine is 10.0.2.3.

We them launch another vm with haproxy.

    
    
    Run sudo apt-get install haproxy
    


This will install haproxy with default settings.
Next to start haproxy as service we have to enable it in the configuration file.

    
    
    vi /etc/default/haproxy
    ENABLED=1
    sudo service haproxy restart
    


Next we haproxy to point to the two servers we setup earlier.Next we move the original configuration of haproxy and keep it as a backup.

    
    
    sudo mv /etc/haproxy/haproxy.cfg /etc/haproxy/haproxy.bak
    


We then create our own configuration file with

    
    
    sudo vi /etc/haproxy/haproxy.cfg
    


Add this to the cfg file.

    
    
    global
        log 127.0.0.1 local0 notice
        maxconn 2000
        user haproxy
        group haproxy
    
    listen appname 0.0.0.0:80
        mode http
        stats enable
        cookie SRVNAME insert
        balance roundrobin
        option httpclose
        option forwardfor
        server server1 10.0.2.2:80 check
        server server1 10.0.2.3:80 check
    



Once this is done a quick restart of haproxy and the haproxy acts as the frontend for the incoming traffic.



