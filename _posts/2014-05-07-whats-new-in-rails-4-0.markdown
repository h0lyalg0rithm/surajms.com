---
author: h0lyalg0rithm
comments: true
date: 2014-05-07 18:34:44+00:00
layout: post
link: http://surajms.com/2014/05/whats-new-in-rails-4-0/
slug: whats-new-in-rails-4-0
title: Whats new in Rails 4.0
wordpress_id: 64
categories:
- Rails
- Ruby
---

You must be wondering why I am writing a blog about Rails 4 even thought it came out nearly 6 months ago.This is mainly because I found some new features and missed some old ones.

One of the most obvious upgrades in rails 4 is that rails now requires ruby 1.9.3+.Which is really great as it helped clean up the core of rails.But as a developer the first change I had to make to my code Strong Parameters.




  * Strong Parameters re-enforces security in by only permitting certain variables through the params field.


  * Turbolinks:Turbolinks is a feature on rails which makes use of javascript to speed up the loading time of the website.The way it works is during the first load of the website.It loads the initial page and takes control over the links.Every time on would click on the link it would make a ajax call in the background and replace the content in the body of the html page.Thereby reducing the requests made to the server and making the website much snappy.This sounds good in theory but in practice this breaks a lot of websites as it has it own onclick and onload events which could break old code.


  * Postgres HStore:Using hstore in postgres has become even easier with the native extension for hstore data.We start with enabling the extenstion in the migration.


	{% raw %}
	<script src="https://gist.github.com/h0lyalg0rithm/1f08a4f1a7f9a32b70f4/f29b39337883b02daf1cae6943bb76712741369b.js"></script>
	{% endraw %}

 We create the attr table in the images table as hstore datatype.

 {% raw %}
<script src="https://gist.github.com/h0lyalg0rithm/1f08a4f1a7f9a32b70f4/16fbf163d479e6e4accc85c9c0525bbdb18bf53d.js"></script>
 {% endraw %}


  * ActiveModel is another important feature in the rails where you can use regular models in rails without the persistence layer.We can even use validations just like a ActiveRecord::Base model.


	{% raw %}
	<script src="https://gist.github.com/h0lyalg0rithm/1c04e8f7c5f0567e6444.js"></script>
	{% endraw %}
