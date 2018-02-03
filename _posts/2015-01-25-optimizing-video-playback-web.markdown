---
author: h0lyalg0rithm
comments: true
date: 2015-01-25 18:23:51+00:00
layout: post
link: http://surajms.com/2015/01/optimizing-video-playback-web/
slug: optimizing-video-playback-web
title: Optimizing video playback for the web
wordpress_id: 306
categories:
- Web
---

Lately I was working on some projects which had videos running in the background.The original videos that I received where high quality but extremely large(1080p videos).Using the chrome debugger, loading a single video on the browser would take atleast 1 hour to download on 250kbps.So I was tasked with re-rendering the video to reduce size.  

To re-render the videos, I used ffmpeg.Its a free software available on all platforms and can we easily accessed via terminal.After tweaking around with the couple of settings I could reduce the video size down significantly.I would also like give a hand of applause to google for moving the web forward.The webm format had the smallest size less than half of the size of the mp4.  

To get ffmpeg installed type

    
    brew install ffmpeg




Here are the configurations I used for rendering the videos
**Webm**

    
    ffmpeg -i time.mp4 -c:v libvpx -c:a libvorbis -pix_fmt yuv420p -quality good -b:v 2M -crf 5 -vf "scale=trunc(in_w/2)*2:trunc(in_h/2)*2" output.webm
    




**mp4**

    
    ffmpeg -i time.mp4 -vcodec libx264 -pix_fmt yuv420p -profile:v baseline -preset slower -crf 18 -vf "scale=trunc(in_w/2)*2:trunc(in_h/2)*2" output.mp4




Just replace time.mp4 with the name of your original video.
