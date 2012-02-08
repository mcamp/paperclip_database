Paperclip Database Storage
==========================

Paperclip Database Storage is an additional storage option for
Paperclip. It give you the opportunity to store your paperclip binary
file uploads in the database along with all your other data.

Requirements
------------

`paperclip_database` depends on `paperclip`

Installation
------------

Paperclip Database Storage is distributed as a gem, which is how it
should be used in your app.

Include the gem in your Gemfile:

    gem "paperclip_database", "~> 2.0"

Or, if you want to get the latest, you can get master from the main
paperclip repository:

    gem "paperclip_database", :git => "git://github.com/softace/paperclip_database.git"
    
If you're trying to use features that don't seem to be in the latest
released gem, but are mentioned in this README, then you probably need
to specify the master branch if you want to use them. This README is
probably ahead of the latest released version, if you're reading it on
GitHub.

For rails 2 you should add this to snippet to your environment.

    # In config/environment.rb
    ...
    Rails::Initializer.run do |config|
      ...
      config.gem "paperclip", :version => "~> 2.4"
      ...
    end

Quick Start
-----------

There is no quick start. You definitely need to understand how to use
paperclip first.

Usage
-----

You use `paperclip_database` by specifying `database` as storage for
your paperclip and create a migration for the additional database
table.

In your model:

    class User < ActiveRecord::Base
      has_attached_file :avatar, 
                        :storage => :database ## This is the essence
                        :styles => { :medium => "300x300>", :thumb => "100x100>" }
    end

There is a migration generator that will create a basic migration for
the extra table.

On the console (rails 2):

    ./script/generate paperclip_database_migration User avatar

On the console (rails 3):

    rails generate paperclip_database_migration User avatar

The generated migration should be sufficient, but yo may consider
adding additional code to it such as `t.timestamps` for adding
standard rails timesstamps or a referential database constraint. If
you add a refferential constraint with the option `ON DELETE CASCADE`,
then you need to add the option `:cascade_deletion => true` to your
paperclip `has_attached_file` declaration.


History
-------

Paperclip Database Storage is heavily inspired by
[this blog](http://patshaughnessy.net/2009/2/19/database-storage-for-paperclip). The
initial source code for that blog is no longer available, but the code
in this gem is based on that initial code.



Copyright
---------

Copyright (c) 2012 Jarl Friis. See LICENSE.txt for
further details.

