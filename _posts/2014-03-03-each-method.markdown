---
author: h0lyalg0rithm
comments: true
date: 2014-03-03 06:34:15+00:00
layout: post
link: http://surajms.com/2014/03/each-method/
slug: each-method
title: Each method
wordpress_id: 36
categories:
- UnderScore
---

Functional programming is the paradigm of programming where the functions are passed as arguments to methods and operations are performed on the function.Underscore makes use of this in a very clean and generic way.

The goal for the each method is to iterate over array or object provided as arguments in the function call.

    
    
    var each = _.each = _.forEach = function(obj, iterator, context) {
        if (obj == null) return obj;
        if (nativeForEach && obj.forEach === nativeForEach) {
          obj.forEach(iterator, context);
        } else if (obj.length === +obj.length) {
          for (var i = 0, length = obj.length; i < length; i++) {
            if (iterator.call(context, obj[i], i, obj) === breaker) return;
          }
        } else {
          var keys = _.keys(obj);
          for (var i = 0, length = keys.length; i < length; i++) {
            if (iterator.call(context, obj[keys[i]], keys[i], obj) === breaker) return;
          }
        }
        return obj;
      };
    


The object/array to be iterated is passed as the first argument.A basic null check is performed and the obj is returned ie null.

    
    if (obj == null) return obj;


We then check if the ecmascript 5's native forEach is present, if it is present we use it instead of implementing our version for each.

    
    if (nativeForEach && obj.forEach === nativeForEach) {
          obj.forEach(iterator, context);
        } 


Javascript has neat way to check to check if a variable is a number object

    
    3===+3

Return true
 The way it works is it passes the + message to the object and === does a equality and type check.

    
    obj.length === +obj.length


Since obj.length is a number ,we perform a check if it a number.which in turn checks if obj is array.
We then loop over each of the items in the array and pass the value to the interator function and call it.

    
    
    for (var i = 0, length = obj.length; i < length; i++) {
            if (iterator.call(context, obj[i], i, obj) === breaker) return;
          }


If obj is an object we get the keys of the objects using underscore's builtin _.keys method.

    
    var keys = _.keys(obj);
          for (var i = 0, length = keys.length; i < length; i++) {
            if (iterator.call(context, obj[keys[i]], keys[i], obj) === breaker) return;
          }


We call the iterator sending the values of the key in the object.

 
