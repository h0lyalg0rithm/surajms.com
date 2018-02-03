---
author: h0lyalg0rithm
comments: true
date: 2014-03-13 05:46:42+00:00
layout: post
link: http://surajms.com/2014/03/map-method/
slug: map-method
title: Map Method
wordpress_id: 46
categories:
- Javascript
- UnderScore
---

Map is another important functional paradigm where you iterate over a object and perform some changes to the original objects.
The way underscore implements the map function is pretty simple.

    
    
      _.map = _.collect = function(obj, iterator, context) {
        var results = [];
        if (obj == null) return results;
        if (nativeMap && obj.map === nativeMap) return obj.map(iterator, context);
        each(obj, function(value, index, list) {
          results.push(iterator.call(context, value, index, list));
        });
        return results;
      };
    
    


The map(aliased as collect) takes the object to interate over as a parameter and the iteration function as the parameter.

    
    
    _.map = _.collect = function(obj, iterator, context) {
    


We create an empty array to store the computation per iteration.We do a simple null check and return the empty error if null.

    
    
      var results = [];
      if (obj == null) return results;
    


We then check if native map is present.If it is present we delegate the map job to the native implementation.
We then run our own iterator using the previously implemented each method and then store the values into the array defined before.Finally we return the array.

    
    
      each(obj, function(value, index, list) {
        results.push(iterator.call(context, value, index, list));
      });
      return results;
    



