---
author: h0lyalg0rithm
comments: true
date: 2014-05-25 04:11:55+00:00
layout: post
link: http://surajms.com/2014/05/messing-around-with-the-twitter-gem/
slug: messing-around-with-the-twitter-gem
title: Messing around with the twitter gem
wordpress_id: 97
categories:
- Ruby
---

This post came out during the Angelhackdubai hackathon.More importantly the angelhack team promised to give away a prize for the person who would tweet the most mentioning #angelhackdubai @thecribb on their twitter feed.

Connecting to twitter was made possible us the [twitter gem](http://rubygems.org/gems/twitter).The gem doesnt take care of the oauth communication with the new twitter 1.1 and above api.It requires you to do the oauth dance provide it the required keys and tokens.

All I had to do is mention my:



	
  1. Consumer Key

	
  2. Consumer Secret

	
  3. Access Token

	
  4. Access Token secret



Writing the following was a quickie but the getting some content for tweet was important as we need to tweet something reasonable.
This brought me to the unirest gem.It is an http post/get request library.
After a quick googling I came across [ICNDB.com](http://www.icndb.com/) which is website with collection of jokes from Chuck Norris.
The site also includes api to make make request programmatically.GET request to http://api.icndb.com/jokes/random would give me a random joke.
Here is the final result

