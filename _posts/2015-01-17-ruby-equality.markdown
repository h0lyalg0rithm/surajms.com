---
author: h0lyalg0rithm
comments: true
date: 2015-01-17 21:18:47+00:00
layout: post
link: http://surajms.com/2015/01/ruby-equality/
slug: ruby-equality
title: Comparisons in Ruby
wordpress_id: 240
categories:
- Ruby
---

Ruby is a dynamic and a true Object oriented language.Due to which ruby has a lot of ways to compare two objects.To be exact it has 4 different ways to compare objects that I am aware of.To understand Ruby objects and equality comparison works lets create a class.
Since I have been playing a bunch of iPad games.Lets create a game object
Lets get some game instances to work with.Now comparing with the **==** operator.
As you can see creating two game object with the same title and comparing them gives you a false result.
This is because the == comparator compares the object's identity.To get the objects identity.Send the object_id message to it.
Now comparing with the equal? operator.
The equal? operator works the same way as the == operator.But unlike the == operator the equal? operator must never be overwritten as it is used internally by ruby to compare object identity.

The eql? operator
The eql operator works a bit differently compared the above two comparators.It compares the hashes between two objects.Even though the final result tends to be similar to ==. Lastly we have the === operator.
The triple equal operator is used in case statement comparison.

So now which operator do I use and when.
1. Double Equal operator:According to ruby conventions, if you want to compare two objects which you own ,you can override the == operator to make it compare properties in your object.

    
    class Game
      attr_reader :title
      def initialize(title)
        @title = title
      end
      def ==(other)
        other.is_a?(self.class) && @title == other.title
      end
    end




When you try to compare 1 == 1.0 you will get true because ruby casts 1 as to a Numeric class and then compares with the 1.0.

2. Triple Equal operator: Like double equal you can use the triple equal operator to compare two objects and also override it to get your desired result.

3.equal?: The equal? operator is used by ruby so use it carefully and never override it.

4.eql?: Like the equal? operator it is better not to override the eql operator and use it to compare both the class and equality of two objects. 
