---
author: h0lyalg0rithm
comments: true
date: 2013-12-28 13:03:50+00:00
layout: post
link: http://surajms.com/2013/12/underscore-setup/
slug: underscore-setup
title: Underscore Setup
wordpress_id: 1351
categories:
- UnderScore
---

When every you include underscore into your code,it does a certain number of checks to make sure that there is no conflict and dependency issues.It also does a check and setup of the parameters that are required to use underscore.


    
    
      var root = this;
      var previousUnderscore = root._;
      var breaker = {};
      var ArrayProto = Array.prototype, ObjectProto = Object.prototype, FuncProto = Function.prototype;
    
      var 
        push = ArrayProto.push,
        slice = ArrayProto.slice,
        concat = ArrayProto.concat,
        toString = ObjectProto.toString,
        hasOwnProperty   = ObjProto.hasOwnProperty;
    
      var
        nativeForEach      = ArrayProto.forEach,
        nativeMap          = ArrayProto.map,
        nativeReduce       = ArrayProto.reduce,
        nativeReduceRight  = ArrayProto.reduceRight,
        nativeFilter       = ArrayProto.filter,
        nativeEvery        = ArrayProto.every,
        nativeSome         = ArrayProto.some,
        nativeIndexOf      = ArrayProto.indexOf,
        nativeLastIndexOf  = ArrayProto.lastIndexOf,
        nativeIsArray      = Array.isArray,
        nativeKeys         = Object.keys,
        nativeBind         = FuncProto.bind;
    
      var _ = function(obj) {
        if (obj instanceof _) return obj;
        if (!(this instanceof _)) return new _(obj);
        this._wrapped = obj;
      };
    
      if (typeof exports !== 'undefined') {
        if (typeof module !== 'undefined' && module.exports) {
          exports = module.exports = _;
        }
        exports._ = _;
      } else {
        root._ = _;
      }
    
      _.VERSION = '1.5.2';
    




    
    var root = this;


Underscore sets root as this ie it sets the root as the windows of the javascript context.

    
    var previousUnderscore = root._;


We save the previous underscore in previousUnderscore.

    
    var breaker = {};


Creates an empty object used later to break out out a loop.

    
    var ArrayProto = Array.prototype, ObjProto = Object.prototype, FuncProto = Function.prototype;


Creates an empty Array object and function to work on later.

    
     var
        push             = ArrayProto.push,
        slice            = ArrayProto.slice,
        concat           = ArrayProto.concat,
        toString         = ObjProto.toString,
        hasOwnProperty   = ObjProto.hasOwnProperty;


Create references for the function so that we dont have to recreate one every time we have to use it.

    
    var
        nativeForEach      = ArrayProto.forEach,
        nativeMap          = ArrayProto.map,
        nativeReduce       = ArrayProto.reduce,
        nativeReduceRight  = ArrayProto.reduceRight,
        nativeFilter       = ArrayProto.filter,
        nativeEvery        = ArrayProto.every,
        nativeSome         = ArrayProto.some,
        nativeIndexOf      = ArrayProto.indexOf,
        nativeLastIndexOf  = ArrayProto.lastIndexOf,
        nativeIsArray      = Array.isArray,
        nativeKeys         = Object.keys,
        nativeBind         = FuncProto.bind;


Create references for the native Ecmascript 5 implementation.

    
    var _ = function(obj) {
        if (obj instanceof _) return obj;
        if (!(this instanceof _)) return new _(obj);
        this._wrapped = obj;
      };


Create a variable _ function.if underscore is already loaded we return it.If _ is not the same as the one loaded.we return a new instance of underscore.



Required to use underscore with node.js.

    
    _.VERSION = '1.5.2'


Sets the version of underscore.

