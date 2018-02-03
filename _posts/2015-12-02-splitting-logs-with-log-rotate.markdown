---
author: h0lyalg0rithm
comments: true
date: 2015-12-02 18:12:19+00:00
layout: post
link: http://surajms.com/2015/12/splitting-logs-with-log-rotate/
slug: splitting-logs-with-log-rotate
title: Splitting logs with log rotate
wordpress_id: 4171
categories:
- DevOps
- Web
---

Last week my colleague Victor from Paack and I were digging through the server to look at the logs.

    
    -rw-rw-r-- 1 dev      dev     3.5M Nov  25 17:33 newrelic_agent.log
    -rw-r--r-- 1 www-data root 1G Nov  25 17:55 nginx.access.log
    -rw-r--r-- 1 www-data root 1G Nov  25 17:55 nginx.error.log
    -rw-rw-r-- 1 dev      dev     0 Apr 30  2015 production.log
    -rw-rw-r-- 1 dev      dev     1G Nov  25 17:33 puma.access.log
    -rw-rw-r-- 1 dev      dev  10G Nov 25 12:03 puma.error.log
    -rw-rw-r-- 1 dev      dev     0 Dec  2 17:34 puma.log
    -rw-rw-r-- 1 dev      dev   50M Dec  2 17:52 sidekiq.log


When we looked at this folder we were shocked.Our log files were a couple of Gigabytes,That was a huge problem, since this could result in slower requests as it logs it.

Are some googling we found that logrotate came part of ubuntu.So though of using it.

The configuration was pretty simple, Logrotate configuration is really cool.It loooks like a bunch of dsls.

    
    /home/dev/apps/paack/shared/log/*.log{
      weekly
      size 500M
      rotate 30
      missingok
      compress
      copytruncate
    }
    


**Weekly**

Runs the script weekly

**size**

Maximum size of the log file

**rotate**

Create a maximum of 30 files.

**missingok**

Ignore error if the file is missng

**compress

**Compress the old logs with gzip

**copytruncate**

Truncate the old log file and create a new one file with the truncated data.



More information can be found on the documentation [website](http://www.linuxcommand.org/man_pages/logrotate8.html)
