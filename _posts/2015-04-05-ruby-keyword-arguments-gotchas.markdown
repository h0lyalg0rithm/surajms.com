---
author: h0lyalg0rithm
comments: true
date: 2015-04-05 19:54:06+00:00
layout: post
link: http://surajms.com/2015/04/ruby-keyword-arguments-gotchas/
slug: ruby-keyword-arguments-gotchas
title: Ruby Keyword Arguments gotchas
wordpress_id: 386
categories:
- Ruby
---

In Ruby 2.0 we were first introduced to keyword arguments.Keyword Arguments are really useful and they clean up the redundant code.

Pre 2.0

    
    def get _stuff(options={})
        first = options.fetch(:first)
        last = options.fetch(:last)
    end


Now

    
    def get_stuff(last:'last',first:'first')
    end


So now we dont need to fetch arguments out of a hash we can just pass it along to the function and it becomes available as arguments.

But with comes at a cost.If you want to specify optional arguments this breaks really easily.Lets take this example.We have a method with two keyword arguments and we want to override the first argument

    
    def get_stuff(first:"first",last:'last')
    end
    
    get_stuff("really_first")
    #ArgumentError: wrong number of arguments (1 for 0)


We get this error because the method expects there to be a key value in the arguments of the method.Moreover ruby spits out its regular ArgumentError wrong number of arguments(1 for 0).

Currently there is not go way to avoid this sort of issue.Nevertheless keyword arguments offer more flexibility and structure to the code.We can also mix together a hash and keyword argument.

    
    def ff(test:1,more:10)
       "#{test} #{more}"
    end
    
    hash = { test: 2, more: 1000}
    
    ff hash # => "2 1000"


This code works well until the hash keys are the same as the keyword argument

    
    hash = { test: 2, more: 1000, extra: 1}
    
    ff hash # => ArgumentError: unknown keyword: extra


Again there is no good way around this apart from cleaning up the arguments before you pass it to the function
