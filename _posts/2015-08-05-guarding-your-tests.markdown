---
author: h0lyalg0rithm
comments: true
date: 2015-08-05 19:39:48+00:00
layout: post
link: http://surajms.com/2015/08/guarding-your-tests/
slug: guarding-your-tests
title: Guarding your tests
wordpress_id: 2301
categories:
- Ruby
---

Automated testing an application can be difficult and time consume.Even after writing your tests you will always have to run it again and again to achieve the red green refactor flow.

To make this task easier the ruby ecosystem has a really powerful and versatile test runner called [Guard](https://github.com/guard/guard).

Guard run like a daemon on your machine and runs tests whenever your code changes.This helps you maintain concentration and focus on the tests and code rather than monotonous manual running of the test.
<!-- more -->


To make this even better Guard uses a Guardfile where you can customize the tasks that Guard you use.

Here is a sample Guardfile for a rails project using rspec to test itself.
{% raw %}
<script src="https://gist.github.com/h0lyalg0rithm/eacf4cb17d32ad1bbfa9.js?file=Guardfile"></script>
{% endraw %}

The first time you run guard your screen would look rather boring like something from the 90's.
To add some color to it update your .rspec file to look something like this.

{% raw %}
<script src="https://gist.github.com/h0lyalg0rithm/eacf4cb17d32ad1bbfa9.js?file=.rspec"></script>
{% endraw %}
