---
author: h0lyalg0rithm
comments: true
date: 2015-09-14 18:02:10+00:00
layout: post
link: http://surajms.com/2015/09/easy-registration-with-devise/
slug: easy-registration-with-devise
title: Easy registration with Devise
wordpress_id: 3021
categories:
- Rails
- Ruby
---

Devise is such a beautiful library.I don't see any reason to write my own authentication component on rails.Moreover Devise allows you to custom every single feature of the library.

Last week I was tasked with creating a registration page for a startup, to make the sign up process simpler we would allow the user to create a company in the same form.Devise made this task very simple.By default devise creates routes for user sign up,but this route would conflict if you have a user resource route.Here is how you can customize the url to use the right controller and route url.
The path_names property sets the registration url to '/users/register' and since we want to create the company relation we use a custom registration controller.
The registration controller's new method overrides the Devise::RegistrationController.

**build_resource({})** and **set_minimum_password_length** enforces the minimum password length and also creates the resource which in this case is the user.
We also create a model for the company.

The method **create** on the other hand just takes the params and generates a user model from it.

The method **sign_up_params** is overridden to allow the company attributes to be used as rails model attributes [More info](http://edgeapi.rubyonrails.org/classes/ActionController/StrongParameters.html).

The view on the other hand is also simple.Just add the relations and devise takes care of the rest.

As you can see the company form field is generated similarly to rails form.
