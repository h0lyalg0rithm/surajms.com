---
author: h0lyalg0rithm
comments: true
date: 2014-05-09 06:49:32+00:00
layout: post
link: http://surajms.com/2014/05/provisioning-a-lamp-stack-with-chef-solo/
slug: provisioning-a-lamp-stack-with-chef-solo
title: Provisioning a LAMP Stack with chef solo
wordpress_id: 54
---

Chef has really speed up the deployment process for me.It basically allows me to define the infrastructure through code which is version control and redeploy-able in seconds.Tody I will working with chef solo through vagrant.
[Vagrant](http://vagrantup.com/) allows me to me create virtual machines which helps me isolate the dev environments from each other.

We start by creating the vagrant file
I will be using librarian chef to manage recipes and cookbooks.We initiate the chef repo with the following command 


    
    librarian-chef init





This creates the the required Cheffile which we will use to manage the cookbooks.

To get the relevant cookbooks we have to run the following command.

    
    librarian-chef install


This will download the cookbooks mentioned in the file above into the cookbooks directory.  

We then can run the knife tool to get the cookbooks installed on to the machine.

    
    knife solo bootstrap vagrant@localhost -p 2222


This will install the chef client on the vagrant box.It will also create a .json file in the nodes directory.Inside the this file we mention the recipes which should be run by the chef client.

Once the file is ready running the knife solo bootstrap command again sets up the lamp stack on the machine.

