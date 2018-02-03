---
author: h0lyalg0rithm
comments: true
date: 2016-09-30 22:18:10+00:00
layout: post
link: http://surajms.com/2016/09/use-roar-take-decorators-next-level/
slug: use-roar-take-decorators-next-level
title: Use roar to take you decorators to the next level
wordpress_id: 272
categories:
- Ruby
---

When writing ruby programs we usually write decorators to extend the methods of a particular object.Using them as form objects is one of the most common uses of a decorator.Ruby makes it simple and easy to create a decorator for a ruby object.

    
    class StuffDecorator
      def initialize(og)
        @og = og
      end
      def stuff
        @og.class
      end
    end


Now we can call the stuff method and it will easily return the class of the original object.

While working on an API backend I came across [**roar**](https://github.com/apotonick/roar).Its a ruby library that allows you to add methods to your ruby object without breaking a sweat.

Here's an example from the docs

    
    require 'roar/decorator'
    class Song
      include ActiveModel::Model
      attr_accessor :title
    end
    
    class SongRepresenter < Roar::Decorator
      include Roar::JSON
    
      property :title
    end
    
    song = Song.new(title: "Medicine Balls")
    
    SongRepresenter.new(song).to_json #=> {"title":"Medicine Balls"}


As you can see the property method calls the original object and returns the response.The best part is now you can get the json serialized version of the object.

If you want to add a custom method you can easily add a method or even override and existing one.

    
    class SongRepresenter < Roar::Decorator
      include Roar::JSON
    
      def more
        represented.title
      end
      property :title
      property :more, exec_context: :decorator
    end


To make things better Roar allows you to serialize your decorator to JSON-API, XML, or even HAL.

All you have to do is include it in the decorator

    
    class SongRepresenter < Roar::Decorator
      include Roar::JSON
      include Roar::XML
    
      property :title
    end
    
    song = Song.new(title: "Medicine Balls")
    
    SongRepresenter.new(song).to_xml #=> "<sonepresenter>\n  <title>test</title>\n</sonepresenter>" 






