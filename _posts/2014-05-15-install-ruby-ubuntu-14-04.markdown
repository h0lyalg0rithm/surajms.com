---
author: h0lyalg0rithm
comments: true
date: 2014-05-15 13:21:45+00:00
layout: post
link: http://surajms.com/2014/05/install-ruby-ubuntu-14-04/
slug: install-ruby-ubuntu-14-04
title: Install Ruby on ubuntu 14.04
wordpress_id: 86
---

After looking online for a long time for a stable and secure way to setup ruby for production.I was forced to install ruby 2.1.2 from source.These were the steps i have to run so get ruby running.
Firstly to build ruby we need the following packages.We need to update your package information using

    
    sudo apt-get update


Once that is done the package manager knows where to get the packages and list is successfully updated.  

To build ruby on the machine we have run the following command which will install the build tools 

    
    sudo apt-get install openssl libreadline-dev curl zlib1g zlib1g-dev libssl-dev libyaml-dev libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev automake libtool bison libcurl4-openssl-dev build-essential


Once that is done we then get ruby on source and extract it a particular directory.Next we run the configure the code to check for dependencies which are required to build.Lastly it is time to build so running the make command to build the binary from source.Make install then installs the software on the computer.

    
    wget http://cache.ruby-lang.org/pub/ruby/2.1/ruby-2.1.2.tar.gz
    tar xzfv ruby-2.1.2.tar.tar.gz
    cd ruby-2.1.2.tar
    ./configure
    sudo make && sudo make install



There you go now you have the latest ruby running on your machine.
