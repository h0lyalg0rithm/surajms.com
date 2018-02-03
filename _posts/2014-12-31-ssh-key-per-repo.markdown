---
author: h0lyalg0rithm
comments: true
date: 2014-12-31 10:34:46+00:00
layout: post
link: http://surajms.com/2014/12/ssh-key-per-repo/
slug: ssh-key-per-repo
title: SSH key per repo
wordpress_id: 227
---

Bitbucket is a good git hosting service especially when they let you create unlimited private repos for free.However bitbucket doesnt let you use the same ssh key with two different users.Now you might be thinking why the hell does he need two different ssh keys.My answer to that is "I wanted to keep my personal and private account seperate"

I am across this post on [stackoverflow](http://stackoverflow.com/questions/22768517/how-to-manage-one-only-key-per-each-git-repository).It pretty much solved my issue.All I had to do was change my ~/.ssh/config file to this..

    
    Host github1
      HostName github.com
      User git
      IdentityFile ~/.ssh/id_repo1
    
    Host github2
      HostName github.com
      User git
      IdentityFile ~/.ssh/id_repo2


You will also have to update the git remote url for the repos.

    
    <code>git remote set-url origin github1:user/repo1
    </code>
