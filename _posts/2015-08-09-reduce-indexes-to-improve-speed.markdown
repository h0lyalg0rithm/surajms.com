---
author: h0lyalg0rithm
comments: true
date: 2015-08-09 22:07:47+00:00
layout: post
link: http://surajms.com/2015/08/reduce-indexes-to-improve-speed/
slug: reduce-indexes-to-improve-speed
title: Reduce indexes to improve speed
wordpress_id: 2491
categories:
- Databases
- Postgres
---

Databases are awesome, they are these blackboxes where data is stored and retrieved at really fast rate.Postgresql is one really fast open source database.

Usually when you want to speed up read speed on your database you usually create indexes on the relevant column.But recently I came to this realization that having more indexes increases the time per insert.

Here is the unscientific benchmark I ran<!-- more -->

{% raw %}
<script src="https://gist.github.com/h0lyalg0rithm/6055b620b3172f71b083.js?file=pg_benchmark.rb"></script>
{% endraw %}

{% raw %}
<script src="https://gist.github.com/h0lyalg0rithm/6055b620b3172f71b083.js?file=database.sql"></script>
{% endraw %}




Here are the results are we run the benchmark script.

Result without index


    ruby bench.rb  0.19s user 0.15s system 12% cpu 2.696 total




Result with the index


    ruby bench.rb  0.22s user 0.18s system 11% cpu 3.448 total
