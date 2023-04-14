---
layout: post
title: Submitting code patches by email
date: 2023-04-14 22:12 +0200
---
Last month I have been working on FFmpeg the swiss army knife for video.While most of the open source repositories manage their code using Git or are directly hosted on Github, FFmpeg has their own hosted git repository and they accept code changes through email.

After trying to share my large PR code to their email address using the process described in their contributions [page](https://ffmpeg.org/developer.html#toc-Submitting-patches-1), I assumed the issue was on my setup as it was the first time I was sending code patches via email.

However today I was contributing a smaller change to project and I tried the patch using the following command
`git format-patch -s -o "outputfolder" --add-header "X-Unsent: 1" --suffix .eml --to ffmpeg-devel@ffmpeg.org -1 1a2b3c4d`

It failed once again as the build system could not apply the patch.
Then I started to dig further into this and came to realize that git comes with a built in feature to send email patches, however it comes part of a seperate package from the git project.
Since my machine was based on Ubuntu, I was able to install it with the following.

`sudo apt-get install git-email sendmail`

Once that is installed I had to set the following in my `~/.gitconfig`.
```
[sendemail]
	smtpserver = smtp.gmail.com
	smtpuser = surajshirvankar@gmail.com
	smtpencryption = ssl
	smtpserverport = 587
```
Then I generated the email and sent it using the following 

`git send-email --to="ffmeg-devel@ffmpeg.org -3` where it sends an email with last 3 commits.

Since I was using my gmail account to send the patch, I had to generate a Google App Password which will be used as the password to login in behalf of my email account.