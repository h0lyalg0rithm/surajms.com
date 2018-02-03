---
author: h0lyalg0rithm
comments: true
date: 2015-06-17 08:38:16+00:00
layout: post
link: http://surajms.com/2015/06/why-i-will-stick-with-lastpass/
slug: why-i-will-stick-with-lastpass
title: Why I will stick with LastPass
wordpress_id: 2071
categories:
- Yapp
---

LastPass is a really awesome password manager.It takes care of generating a password,saving and syncing it with all your devices.

But yesterday they sent an email explaining that they were hacked.Hacking really popular these days,on an average there are about 9 defacements that happen everyday.But after going through the email.I was happy.

You might be wondering ,why is he so happy.The reason I was happy was due to the architecture LastPass had built to perform all the above mentioned features.

The way LastPass works is it uses a really secure encryption algorithm pbkdf2.As part of this algorithm the content can be encrypted multiple times like a chain.Lastpass made use of this technique really well.

They set the iteration count to 100000, which meant that if you want to decrypt it you have to perform it 100000 times to receive the decrypted content.

Moreover all of the keys that used for encryption is derived from your pass phrase.so if you have a really long and random password, it will make it near to impossible to decrypt the passphrase.They don't save the keys on their server.
Having said all of this,I am not gonna change my password,the hacker can have my encrypted blob and hope they are happy cracking it on their ASIC devices
