---
author: h0lyalg0rithm
comments: true
date: 2015-12-07 20:15:54+00:00
layout: post
link: http://surajms.com/2015/12/move-kitematic-disk-to-a-different-drive/
slug: move-kitematic-disk-to-a-different-drive
title: Move kitematic disk to a different drive
wordpress_id: 4223
categories:
- DevOps
- Docker
---

Today I upgraded one of my old macs with an SSD.The SSD is freaking fast.But since the SSD was less than half the size of the existing HDD, I thought it would be good idea to move the docker host machine to the HDD instead of the SSD

Doing this was pretty simple.

First make sure the virtual machine was switched off.Then click on setting and then on the storage button which is the 3rd from the left.

[![1](http://surajms.com/wp-contents/uploads/2015/12/1.png)](http://surajms.com/wp-contents/uploads/2015/12/1.png)

Select the disk.vmdk and click on the floppy icon with the minus button.For those who dont know what a floppy is [click here](https://www.google.ae/search?q=floppy+disk&source=lnms&tbm=isch&sa=X&ved=0ahUKEwiGvZ76xcrJAhWF2RoKHaUkDAcQ_AUIBygB&biw=1440&bih=725).Then click ok to save it.

Next open the following path in finder.  **~/.docker/machine/machines/default**

Next copy the disk.vmdk drive to the HDD.

Once it is copied you can delete it from this folder.

Now we need to connect the Virtual drive back to the virtual machine.

Then click on File and select Virtual Media Manager.

[![2](http://surajms.com/wp-contents/uploads/2015/12/2.png)](http://surajms.com/wp-contents/uploads/2015/12/2.png)

Then click on the remove button from the virtual drive.If you dont follow this setup virtualbox will not allow you to connect the drive to the virtual machine.

[![3](http://surajms.com/wp-contents/uploads/2015/12/3.png)](http://surajms.com/wp-contents/uploads/2015/12/3.png)

Now you are ready to connect the virtual drive to the virtual machine.Click on the setting button for the virtual machine.Select storage and click on the plus hdd button and select the virtual drive.

[![4](http://surajms.com/wp-contents/uploads/2015/12/4.png)](http://surajms.com/wp-contents/uploads/2015/12/4.png)

Now the kitematic will use the same virtual machine and it will not notice a difference.
