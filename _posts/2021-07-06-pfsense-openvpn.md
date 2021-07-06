---
layout: post
title: PfSense OpenVPN
date: 2021-07-06 05:21 +0200
---
Last month I ended up purchasing a second hand server to use for my hobby projects.One of those projects was to run PfSense as a firewall/Network router.

Here is how my network is setup at the moment.

![](/wp-contents/uploads/2021/07/network.png)

My goal would be to able to connect to the server from both inside my home network.
Here are the steps I followed
- Installed PfSense on the server
- Setup OpenVPN on Pfsense.
- Port forward OpenVPN port(default 1194) from router to server.

But when I was inside the my 192.168.31.0/24 network.After banging my head a couple of times not able to connect.
I began to dig into the firewall settings and found a firewall rule that was setup by default.
I had to disable configuration in the rule and the connection was successfully established.

![](/wp-contents/uploads/2021/07/firewall-rule.png)

![](/wp-contents/uploads/2021/07/firewall-rule-check.png)

