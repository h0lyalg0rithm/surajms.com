---
author: h0lyalg0rithm
comments: true
date: 2016-10-01 22:17:09+00:00
layout: post
link: http://surajms.com/2016/10/managing-multiple-version-elixir-erlang/
slug: managing-multiple-version-elixir-erlang
title: Managing multiple version of elixir and erlang
wordpress_id: 4861
categories:
- Elixir
---

For a while I have been working on different elixir projects each with their own set of dependencies both on erlang and elixir.

Switching between is made simple using evm and kiex.
Evm - Erlang version manager is used to switch between the different versions of Erlang.
Kiex - Elixir version manager is used to switch between the different versions of Elixir.

Having these tools installed on the computer saves a bunch of time installing erlang & elixir.But remembering to switch between them for each project was difficult to remember.So the quick and naive way to solve this would be to use a **.er** file inside the project directory.This file would be sourced into the shell.

    
    evm use OTP_18.1  # Sets the erlang version to 18.1
    kiex use 1.2.5  # Sets the elixir version to 1.2.5


Another quick tip evm doesnt install erlang with SSL.To install it run the following.OpenSSL is installed on the system using Homebrew.If you are using the default openssl, change the directory.

    
    evm install OTP_18.1 --with-ssl=/usr/local/opt/openssl




With some zsh magic now the shell will switch the version of erlang and elixir.

    
    function set_erlang_version() {
       if [ -f .er ]; then
         source .er
       fi
     } 
    chpwd_functions=(${chpwd_functions[@]} "set_erlang_version")
