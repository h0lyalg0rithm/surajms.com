---
author: h0lyalg0rithm
comments: true
date: 2015-12-12 17:11:17+00:00
layout: post
link: http://surajms.com/2015/12/vim-day-part-1/
slug: vim-day-part-1
title: Vim a day - Part 1
wordpress_id: 4301
categories:
- Vim a day
---

This is the first blog post from the _Vim a day series_.

The post is about the plugin ctrlP which is available [here](https://github.com/ctrlpvim/ctrlp.vim).This plugin is really useful since it lets you jump between files really quickly.

If you are using Vundle, its really easy to install.

    
    Plugin 'kien/ctrlp.vim'
    


Now typing control + p does a quick fuzzy search in the current directory.Some of the quick shortcuts that I came across.

<c-t> Open the file in a new tab

<c-v>Open the file as vertical split

<c-x>Open the file as horizontal split



Lastly there is an essential configuration that could really speed up the fuzzy search

    
    let g:ctrlp_user_command = ['.git/', 'git --git-dir=%s/.git ls-files -oc --exclude-standard']


This ignores the files in .git folder and the .gitignore file.
