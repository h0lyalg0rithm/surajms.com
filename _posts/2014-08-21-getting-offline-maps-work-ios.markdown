---
author: h0lyalg0rithm
comments: true
date: 2014-08-21 15:40:08+00:00
layout: post
link: http://surajms.com/2014/08/getting-offline-maps-work-ios/
slug: getting-offline-maps-work-ios
title: Getting offline maps to work with iOS
wordpress_id: 143
categories:
- iOS
- Maps
---

The current project I am working with required me to have maps to work offline.The gist of the app was it would connect to a hardware device running a server.Since most common use case for the app was at remote location, having offline maps was essential.

After some quick googling I came across mapBox,it is a startup which works on creating open source mapping tools for developers.

Getting back to the meat of this post,
To get the maps to work on mapbox i have to create maptiles which is a combination of sql statements which is required by map box to generate maps.
The most essential tool for creating the maps was homebrew.

I then had to install postgres which was pretty easy with homebrew.

    
    brew install postgresql
    initdb /usr/local/var/postgres -E utf8
    postgres -D /usr/local/var/postgres
    createuser -d -P postgres


The previous commands install postgres ,setups up initial databases,creates a new user called postgres and starts the database.

Since the default install of postgres doesn’t understand gis(Geographic Information System) data we had to install postgis (extension for postgres).Brew comes back to scene making it trivially easy to install.

    
    brew install postgis


Next we create a database on postgres to save the map data.

    
    psql -U postgres 
    CREATE DATABASE osm;
    c osm;
    create extension postgis;
    dt


If you don’t see any table means that the extension has not been loaded correctly.To fix it you might have run the following

    
    psql osm < /usr/local/Cellar/postgresql/9.3.5/share/postgresql/extension/postgis--2.1.3.sql


_ Note the postgresql & potgis version number depends on the version you have installed;_

Next you can download compressed binary map data from [http://metro.teczno.com/](http://metro.teczno.com/) or the updated [https://mapzen.com/metro-extracts/](https://mapzen.com/metro-extracts/).
Download the pbf file of the particular location.

Once you have downloaded the file you will also require osm2pgsql which converts the binary pbf file to sql statements

    
    osm2pgsql -c -G -d test -S /usr/local/share/osm2pgsql/default.style dubai-abu-dhabi.osm.pbf


_Note: replace test with name of the database you created on postgres.Also change dubai-abu-dhabi.osm.pbf to the file you just downloaded_

The next steps would let will create world map (just outline no details/layers)

    
    wget https://github.com/mapbox/osm-bright/zipball/master
    wget http://data.openstreetmapdata.com/simplified-land-polygons-complete-3857.zip
    wget http://data.openstreetmapdata.com/land-polygons-split-3857.zip


Once you have downloaded these files extract the osm-bright zip first.Then extract the other two files.

Copy the extracted file to the shp directory.
Then edit the configure.py file in the mapbox-osm-bright folder
**Edit the config[“postgis”] usually along line 21-25**
** Also edit the map.py file.Change defaultconfig[“postgis”] to our environment.(Usually at line 81-86)**

Before you run that download tilemill and run it.

Once you are done with that.Run the python script make.py
This will create a project file for the tilemill app.
The project name is called osm-bright open it and select export to maptile to create one.
You now have an offline map file which will work with mapbox.




