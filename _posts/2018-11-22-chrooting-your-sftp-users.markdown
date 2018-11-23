---
layout: post
title: "Chrooting your sftp users"
date: "2018-11-22 23:15:03 +0100"
---
It had been a while  since we last upgraded our [website](https://paack.com).We had decided to outsource the website development to an external web development agency.

The website was built on wordpress, so we had to setup an sftp account for the developers to upload and edit the wordpress template.

Since we also host other websites like our api documentation on the same server as the current website, we had to ensure the external developers didnt have access to the other website files and directories.

Since we used nginx as the webserver, we used the standard web directory structure `/var/www/html/` to upload the individual websites.

To restrict the users access to other directories in the system we had to setup [`chroot`](https://en.wikipedia.org/wiki/Chroot)

- First we create a the website directory  
  `mkdir -p /var/www/html/paack.co/wordpress`
- Create a new user adding him to the www-data group.  
`useradd -d /var/www/html/paack.co/wordpress -g www-data newuser`
- We need to restrict the root folder `/var/www/html/paack.co` by setting the owner as root  
`sudo chown root:root /var/www/html/paack.co`
- To allow the new user to write to the new directory we set the folder permission  
`sudo chmod 755 /var/www/html/paack.co`
- Now we need to allow the user to connect through sftp   
  We need to update the `/etc/ssh/ssh_config` and comment out the following line  
  `Subsystem sftp /usr/lib/openssh/sftp-server`  
  We need to add the following right after the commented line  
  `Subsystem sftp internal-sftp`
- Finally at the end of the file we need *add* the configuration to allow the user to connect  
```
Match User newuser
PasswordAuthentication yes
ForceCommand internal-sftp
ChrootDirectory /var/www/html/paack.co/wordpress
X11Forwarding no
AllowTcpForwarding no
```
The configuration allows the user to connect via sftp.
- `sudo service ssh restart` to restart the ssh deamon.

Other issues I came across
- ssh_config is super strict about the order of the configuration. If the `UsePAM` config appears after the `Match` configuration this will result in the ssh restart error.
