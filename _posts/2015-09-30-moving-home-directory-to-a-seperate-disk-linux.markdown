---
author: h0lyalg0rithm
comments: true
date: 2015-09-30 23:11:42+00:00
layout: post
link: http://surajms.com/2015/09/moving-home-directory-to-a-seperate-disk-linux/
slug: moving-home-directory-to-a-seperate-disk-linux
title: Moving home directory to a seperate disk linux
wordpress_id: 2961
categories:
- DevOps
---

While working on the [Paack](http://paack.co) application I came across the issue where the main hard disk on the machine was getting full.Mostly due to the fact that Capistrano saves atleast 25 of the last deployments on the server.That meant the assets and the precompiled data, would all be written on the same drive.At the time when I looked at the computer, the system had about 36% drive space free.This was a huge cause of concern since I didn't want to deal with the limited storage issue.

So I began looking at the azure documentation/reference on setting up extra hdd on a single virtual machine.Azure restricts the number of drives you can attach per virtual machine based the tier of the virtual machine.

<!-- more -->

Since my machine supported two.I attached two drives each of 1 TB.Now came the time to migrate the data from the home directory to the other hdd.

Here are the steps I followed to set things up.



	
  * Firstly the disk which are attached need to be partitioned and formatted for the OS to use.I partitioned the drive using fdisk.I told fdisk to create a single partition on the whole drive.

	
  * I then used mkfs.ext4 to set the correct file system headers on the partition.

	
  * How was time to move the directories.Firstly I had to mount the partition on a new directory.

	
  * I created a folder under /media/home and then mounted it using the **mount** command.

	
  * We then copy all the files from the /home/ directory to /media/home directory

    
    sudo rsync -aXS --exclude='/*/.gvfs' /home/. /media/home/.




	
  * Once we are done copying, we need to edit the file that tells the operating system which partitions to mount during system startup.The file uses the disk uuid to detect which disk to mount.

	
  * To find out the uuid of your drive use the **blkid **command.Note it requires root permission.

	
  * Now edit the /etc/fstab and include the following line to mount the /home/ directory

    
    UUID=xxxxxx   /home    ext4         defaults       0       2


(Where xxxxxx is the uuid of your drive)

	
  * Next reboot the device for the move to take place


