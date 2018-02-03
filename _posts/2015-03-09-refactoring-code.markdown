---
author: h0lyalg0rithm
comments: true
date: 2015-03-09 19:34:19+00:00
layout: post
link: http://surajms.com/2015/03/refactoring-code/
slug: refactoring-code
title: Refactoring code 
wordpress_id: 367
---

Today I was working with one of the startups at the cribb on their project to clean up their code and fix a critical issue with the it.

The codebase was not large but it was kinda modular.Being an MVP the product worked, it was serving a bunch of users.Unfortunately the code most important for them was a bit buggy.It was creating multiple connections to the database on a single request.This problem was exaggerated by the limit the hosting provider put on the number of database connections to it.

So we sat down to fix the code.Unfornately the code didn't have test ,I wouldn't blame them as it was an MVP.So we manually tested the website.We turned on debug messages and we were off fixing the issue.

The main problem arose at the database connection class.This class was used to create connections to the database and every instance of this class would start another connection to the database.

The obvious solution that came to mind was to write a singleton, which is mostly frowned upon.But we decided to do it anyways.Moreover it had been a really long time since I touched PHP code.So after going through  some old code from other projects.I found realized how easy it is to forget such stuff.Code which I once thought I was a master off was completed erased from my head.Lucky the concepts still stayed with me.

Fixing the issue on the database was straight forward we created a singleton database connection class which other models would use to query for information.This brought down the connection count to just one as it is supposed to be.

Singletons is well know for being an anti pattern as it is makes testing difficult or it being used as a global variable.But in this case the singleton pattern was really benificial.
