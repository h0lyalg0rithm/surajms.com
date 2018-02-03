---
author: h0lyalg0rithm
comments: true
date: 2015-04-06 18:44:56+00:00
layout: post
link: http://surajms.com/2015/04/setting-up-ssl-on-an-apache2-box/
slug: setting-up-ssl-on-an-apache2-box
title: Setting up SSL on an apache2 box
wordpress_id: 403
categories:
- DevOps
- Web
---

Apache 2 is a well know server for linux.Setting up an SSL certificate on it is very simple  and straightforward.

Firstly we need an SSL certificate,We can get it from numerous online SSL providers or we could generate one ourself.

To generate a 2048 bit key.

    
    sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt


This will create your public ssl certificate and a private key.

Next we have to enable ssl module for apache2

    
    sudo a2enmod ssl


Once have this enabled,Lets add the certificate to all of the websites running on the server.On apache2 you can find the websites on /etc/apache2/sites-available/.Lets change the default-ssl.conf file on the /etc/apache2/sites-available/default-ssl.conf.

Just change a couple to lines in the file.

    
    SSLEngine on
    SSLCertificateFile /etc/apache2/ssl/apache.crt
    SSLCertificateKeyFile /etc/apache2/ssl/apache.key


These configurations tell apache which certificate to use and which key goes along with it.All we have to do now is enable the configuration

    
    sudo a2ensite default-ssl.conf


And then to restart the apache2 server

    
    sudo service apache2 restart



