---
author: h0lyalg0rithm
comments: true
date: 2015-02-15 18:16:22+00:00
layout: post
link: http://surajms.com/2015/02/absolute-vs-relative-positioning/
slug: absolute-vs-relative-positioning
title: Absolute vs relative positioning
wordpress_id: 268
categories:
- CSS
---

Understanding relative and absolute positioning in CSS didn't come easily to me when I first started building websites.Now ages after building more websites than I count.I have gotten used to way the browser positions stuff.

Before I talk about absolute/relative position I need to explain what static position is.
[codepen_embed height="468" theme_id="0" slug_hash="dPdRvd" default_tab="result" user="h0lyalg0rithm"][/codepen_embed]


By default every element in the DOM is positioned static.Which means every element appears one after the other in the order they were written in the body tag.

So what is absolute position?Absolute position is where you set the position of the current element relative to the first parent element.
[codepen_embed height="500" theme_id="0" slug_hash="GgQEEw" default_tab="result" user="h0lyalg0rithm"][/codepen_embed]
Relative position on the other hand sets the element relative to the parent.
[codepen_embed height="500" theme_id="0" slug_hash="bNLRWy" default_tab="result" user="h0lyalg0rithm"][/codepen_embed]

So we can build awesome stuff by combining the two.
[codepen_embed height="268" theme_id="0" slug_hash="OPQgjq" default_tab="result" user="h0lyalg0rithm"][/codepen_embed]

