Neo4jrb::Paperclip - Making Paperclip play nice with Neo4j.rb 3.0
================================================================

This gem is based on [mongoid-paperclip 0.0.4](https://github.com/meskyanichi/mongoid-paperclip). It is a fork of Leo Lou's original gem, updated for Neo4j.rb 3.0. It is platform-independent and compatible with Paperclip 4.2.0.

As the title suggests: `Neo4jrb::Paperclip` makes it easy to hook up [Paperclip](https://github.com/thoughtbot/paperclip) with [Neo4j.rb](https://github.com/andreasronge/neo4j).

This is actually easier and faster to set up than when using Paperclip and the ActiveRecord ORM.
This example assumes you are using **Ruby on Rails 4** and **Bundler**.


Setting it up
-------------

Simply define the `neo4jrb-paperclip` gem inside your `Gemfile`, pulling from subvertallchris/neo4jrb-paperclip. Additionally, you can define the `aws-sdk` gem if you want to upload your files to Amazon S3. *You do not need to explicitly define the `paperclip` gem itself, since this is handled by `neo4jrb-paperclip`.*

**Rails.root/Gemfile - Just define the following:**

    gem "neo4jrb-paperclip", github: 'subvertallchris/neo4jrb-paperclip', require: "neo4jrb_paperclip"
    gem "aws-s3"

Next let's assume we have a User model and we want to allow our users to upload an avatar.

**Rails.root/app/models/user.rb - include the Neo4jrb::Paperclip module and invoke the provided class method**

    class User
      include Neo4j::ActiveNode
      include Neo4jrb::Paperclip

      has_neo4jrb_attached_file :avatar
      validates_attachment_content_type :avatar, content_type: ["image/jpg", "image/jpeg", "image/png", "image/gif"]
    end


That's it
--------

More or less. See [Paperclip's documentation](https://github.com/thoughtbot/paperclip/wiki) for additional instructions. 
Invoking the `has_neo4jrb_attached_file` method will automatically define the necessary `:avatar` fields for you in the background.

Known issues
------------

File size returns 0 - [paperclip issue](https://github.com/thoughtbot/paperclip/issues/100)

Related Links
------------

* [mongoid-paperclip](https://github.com/meskyanichi/mongoid-paperclip)
* [Neo4j.rb](https://github.com/andreasronge/neo4j)
* [Paperclip](https://github.com/thoughtbot/paperclip) 
