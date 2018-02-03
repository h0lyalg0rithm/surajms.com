---
author: h0lyalg0rithm
comments: true
date: 2014-02-08 17:19:35+00:00
layout: post
link: http://surajms.com/2014/02/writing-a-rake-task-in-rails/
slug: writing-a-rake-task-in-rails
title: Writing a rake task in rails
wordpress_id: 25
categories:
- Rails
- Ruby
---

Writing a rake task in rails i pretty simple.In this post i will describe creating a rake task to reset the password of every user on the system.Maybe you had a breach and to prevent identity theft you reset the users password and send it to the user through his email address.

To create a rake task we firstly have to namespace it so that it doesnt conflict with existing rake tasks and it also helps us keep our code more modularized.


    
    
    /// lib/tasks/defcon.rake
    require 'securerandom'
    namespace :defcon do
      desc 'Reset users emails'
      task :got_hacked do
        begin
          User.all.each do |user|
            password = SecureRandom.hex.slice(0,10)
            user.password = password
            user.save
            UserMailer.reset_password(user,password)
          end
        rescue Exception => e
          puts "#{e.message} occured"
        end
      end
    end
    


We first require the securerandom library.This is required to generate some random password for each user.
We namespace the task with a name,for now i have called defcon.
The task name here is got_hacked which runs once the we type rake defcon.got_hacked so if in case we get hacked we can instantly reset the password for all the users in our system.
Inside the task we have begin and rescue block,this is make sure that we catch any exception that occurs and output it on the screen.
So the regular flow of the program is as such.We loop through all the users in the system (assuming there is a user model).We generate a random password and set that as the password for the current user in the loop.We save the password in the database and then send them a email stating that their password has been reset.
The UserMailer class for sending the email is given below

    
    
    /// app/mailer/user_mailer.rb
    class UserMailer < ActionMailer::Base
      def reset_password(user,password)
        mail(to: user.email, subject: "We got hacked", from: "xxx@xxxx.com")
      end
    end
    


The view for the email

    
    
    /// app/view/user_mailer/reset_password.html.erb
    Dear <%= user.name %>,
    We have been hacked.Here is you new password for the account.
    password : <%= user.password %>
    
