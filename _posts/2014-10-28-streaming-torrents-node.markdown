---
author: h0lyalg0rithm
comments: true
date: 2014-10-28 16:53:18+00:00
layout: post
link: http://surajms.com/2014/10/streaming-torrents-node/
slug: streaming-torrents-node
title: Streaming torrents with node
wordpress_id: 174
categories:
- Yapp
---

[PopCorn](https://popcorntime.io/) time is free app which lets users stream movies and tv shows for free.For the geek in me, the best part about the app is that it is open source and build on top of node making it cross platform.

After taking a look at the [code](https://git.popcorntime.io/stash/projects/PT/repos/popcorn-app/browse/package.json) to figure out how exactly the app downloads torrents.I learnt about [peerflix](https://github.com/mafintosh/peerflix) module.This module takes care of downloading the torrent.

After going through the [README](https://github.com/mafintosh/peerflix) I noticed you can use peerflix as a commandline tool for any kind of torrent file including magnet links.From now on Peerflix has become my definitive  way to stream tv shows.

    
    peerflix "magnet:?xt=urn:btih:ef330b39f4801d25b4245212e75a38634bfc856e"   --vlc



