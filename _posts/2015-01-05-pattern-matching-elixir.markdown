---
author: h0lyalg0rithm
comments: true
date: 2015-01-05 07:01:43+00:00
layout: post
link: http://surajms.com/2015/01/pattern-matching-elixir/
slug: pattern-matching-elixir
title: Pattern matching in Elixir
wordpress_id: 242
categories:
- Elixir
- Ruby
---

Elixir is a ruby like language built on top of the Erlnag VM.It has some really nice features which makes writing recursive functions a breeze.Here is a defacto example to write a factorial program in elixir.

As we can see having guards and pattern matching makes recursive functions a breeze

{% raw %}
<script src="https://gist.github.com/h0lyalg0rithm/7eaeb6b26b243cc05268.js?file=factorial.ex"></script>
{% endraw %}


Comparing that too ruby,the LOC are more but the code is more readable.

{% raw %}
<script src="https://gist.github.com/h0lyalg0rithm/7eaeb6b26b243cc05268.js?file=factorial.rb"></script>
{% endraw %}

Comparing it to some ugly javascript.

{% raw %}
<script src="https://gist.github.com/h0lyalg0rithm/7eaeb6b26b243cc05268.js?file=factorial.js"></script>
{% endraw %}
