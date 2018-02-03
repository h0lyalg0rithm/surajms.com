---
author: h0lyalg0rithm
comments: true
date: 2014-11-14 10:35:52+00:00
layout: post
link: http://surajms.com/2014/11/automating-web-development-environment/
slug: automating-web-development-environment
title: Automating your web development environment
wordpress_id: 101
categories:
- CSS
- Grunt
- Javascript
---

A year ago I was working on a project.It was a standard HTML and CSS project.Since it was side project I had about an hour to work on it every day.

The first few weeks the project CSS was fairly large each file with about ~1000 lines of hate.But after a couple of weeks the CSS was now about 2000 lines and reusing CSS had become cumbersome.

Wow it's 2013 and I was not using a build process for my saas files.I got so tired of running compass manually on the files and waiting for it complete so I could refresh the browser tab.

I took a stab at grunt.Grunt is a task runner for JavaScript.It has a huge collection of plugins which can be installed and used to create your build pipeline.

Grunt is cross platform and it runs on nodes.So the first thing I had to set up was node.I suggest getting the latest version of node.With every node project you need to use a package manger as it takes care of downloading and dependency management for the packages.

Grunt includes a command line tool which has to be installed globally


<blockquote>npm install -g grunt-cli</blockquote>


You need to create a package .json file by running the **npm init** command in your shell.You will also need to create a Gruntfile.js file in the project root directory.

Add the following dependencies to **package.json** file.

    
    {
      "name": "Demo site",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "author": "",
      "devDependencies": {
        "grunt": "^0.4.5",
        "grunt-contrib-compass": "^1.0.1",
        "grunt-contrib-watch": "^0.6.1",
        "grunt-express": "^1.4.1",
        "grunt-open": "^0.2.3",
        "matchdep": "^0.3.0"
      }
    }
    




You then need to add the following tasks to Gruntfile.

    
    module.exports = function(grunt){
      require('matchdep').filterDev('grunt-*').forEach(grunt.loadNpmTasks);
      grunt.initConfig({
        express: {
        all: {
            options: {
              bases: ['/Users/surajshirvankar/Desktop/vk.ae/'],
              port: 8080,
              hostname: "0.0.0.0",
              livereload: true
            }
          }
        },
        compass:{
          dev:{
            options: {
              sassDir: 'sass',
              cssDir: 'css'
            }
          }
        },
        watch: {
          compass: {
            files: ['sass/*'],
            tasks: ['compass:dev']
          },
          all: {
              files: ['*.html', 'css/*.css'],
              options: {
                  livereload: true
            }
          }
        },
        open: {
          all: {
            path: 'http://localhost:8080/index.html'
          }
        }
      });
      grunt.registerTask('default', ['express','open','watch']);
    }




You are now done.Just run grunt and it takes care of starting a local server,live-reloading if you change files and build your CSS.
