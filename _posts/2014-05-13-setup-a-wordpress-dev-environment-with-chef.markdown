---
author: h0lyalg0rithm
comments: true
date: 2014-05-13 19:34:43+00:00
layout: post
link: http://surajms.com/2014/05/setup-a-wordpress-dev-environment-with-chef/
slug: setup-a-wordpress-dev-environment-with-chef
title: Setup a wordpress dev environment with chef
wordpress_id: 1361
categories:
- Chef
- DevOps
---

I just recently created a cookbook for wordpress.The cookbook will automatically download and set up the database for you.To get started on using the cookbook.
1.If you are using librarian just add this line to the Cheffile.

    
    cookbook 'wordpress', :git => 'https://github.com/h0lyalg0rithm/wordpress-cookbook'


otherwise you can download the cookbook from the [here](https://github.com/h0lyalg0rithm/wordpress-cookbook) and extract it into your cookbooks directory.
2.Next just add the following to the run list or to the role file.

    
    recipe[wordpress]
