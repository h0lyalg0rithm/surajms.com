---
author: h0lyalg0rithm
comments: true
date: 2015-08-10 16:50:42+00:00
layout: post
link: http://surajms.com/2015/08/postgres-table-inheritance-causing-missing-id-rails/
slug: postgres-table-inheritance-causing-missing-id-rails
title: Postgres table Inheritance causing missing id in rails
wordpress_id: 2281
categories:
- Postgres
- Rails
---

Postgres is a really powerful database with a lot of features, One of the most important features which is very rarely found in other databases is "Table inheritance"

Table inheritance is very similar to class inheritance of OOP.In Table inheritance you have a parent table which is inherited by another table with extra columns in it.

By default the pg gem doesnt support table inheritance.

In the current project that I am working on, the business logic required the user to have template using which he could create items.This is where table inheritance shines.It allowed me to create the template model which contained all the generic attributes for the item.So everytime I would update the template the relevant model for the template would also be updated.
<!-- more -->









Here is the sql I had to write to get it working in my current project



But if wanted to update the item model I would face an error that id was not found.So I took a look the database and realized that table inheritance caused the items table to share the id column with the item_templates table.

Here is the quick fix 



By setting the primary key property on item model.Rails was able to understand that the primary key was from the parent table not from current table.

