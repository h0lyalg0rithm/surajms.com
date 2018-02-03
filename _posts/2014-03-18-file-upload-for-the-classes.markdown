---
author: h0lyalg0rithm
comments: true
date: 2014-03-18 19:16:15+00:00
layout: post
link: http://surajms.com/2014/03/file-upload-for-the-classes/
slug: file-upload-for-the-classes
title: File upload for the classes
wordpress_id: 49
categories:
- Rails
- Ruby
---

With one of our products in our company we were given the task of building a file uploading system which would take different type of files and upload it to our server.Instead of creating a separate class for each file and having different methods to upload the file, we instead opted for a creating a polymorphic class which can be used with different classes with the _has_many_ relation.

First we begin by creating a migration with the polymorphic relations in the database 

    
    rails g migration CreateAssetsTable


We then fill in the migration 

    
    
    class CreateAssetsTable < ActiveRecord::Migration
      def change
        create_table :assets do |t|
          t.string :type
          t.references :attachable, polymorphic: true
          t.timestamps
        end
      end
    end
    


We then run the migration

    
    rake db:migrate


This sets up the assets table with 6 columns.Id,Type,attachable_id,attachable_type,created_at and updated_at.The important columns for the polymorphic relation are the attachable_type and attachable_id.This sets up the relation between other classes and the asset class at the database level.
Next we create the model for this class

    
    rails g model asset


This will create the model class and set us up with an empty model class.We then will in the polymorphic relation.

    
    
    class Asset < ActiveRecord::Base
      belongs_to :attachable, polymorphic: true
    end
    


Just like in the migration the polymorphic relation is the most important feature of this class.

Now that we have the asset class ready we then create other class which will use this relation.
Example:

    
    
    class Users < ActiveRecord::Base
       has_many :avatars, as: :attachable, class_name: "Asset"
    end
    


The has many sets up the has_many relation with the user model.So now the user has many avatars which refers to the assets model for the asset with type avatar.
Now that we have dealt with the polymorphic nature of the classes,It becomes very easy to add the upload module to the asset class using the paperclip gem by thoughtbot.
We add the gem to the gem file

    
    gem 'paperclip'



    
    bundle install -j4


Next we generate migration for the assets table to hold your new data

    
    
    class AddAttachmentToAsset < ActiveRecord::Base
      def up
        add_attachment :assets, :file
      end
      def down
        remove_attachment :assets, :file
      end
    end
    



    
    rake db:migrate


We the add the has_attached_file to the Asset class

    
    
    class Asset < ActiveRecord::Base
      belongs_to :attachable, polymorphic: true
      has_attached_file :file
    end
    


Since version 4 of paperclip content validation is required by default.
So we also add a simple image file validation using regex

    
    
       validates_attachment_content_type :file, content_type: /Aimage/.*z/
    


This check if the mime type of the file contains image/ followed by the format.
Now we have a generic file upload class.

