---
author: h0lyalg0rithm
comments: true
date: 2016-03-02 18:35:17+00:00
layout: post
link: http://surajms.com/2016/03/create-custom-instances-cloudatcost/
slug: create-custom-instances-cloudatcost
title: Create custom instances on cloudatcost
wordpress_id: 4651
---

Last month I released a plugin for [fog](http://github.com/fog/fog), a ruby gem that helps you manage servers on different cloud providers.

Cloudatcost is one of those unique providers where you can get a server for lifetime so basically you will don't have to worry about paying for the machine every month.However the ui to create the virtual machine is extremely horrible.But then I came across their api. The noticed you can set the ram capacity for each machine through it.This is unlike most other providers who have a fixed size for the virtual machine.

So here is how i used fog-cloudatcost to setup multiple vpn servers.

    
    require 'fog'
    
    cac = Fog::Compute.new({
      :provider  => 'CloudAtCost',
      :email     => 'example@email.com',         # Your email address
      :api_key   => 'poiuweoruwoeiuroiwuer', # your API Token   
    })
    # Then we get the OS templates available
    
    cac.templates.each do |image|
      puts image.id
      puts image.detail
    end
    
    server = cac.servers.create :cpu => 'foobar', # 1, 2, 4 
                                :ram  => 1024, # multiple of 4 min 512
                                :storage => 10, # 10G
                                :template_id => 75 #Template id
    
    
