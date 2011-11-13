---
layout: post
title: "Cascading deletion with Carrierwave and Mongoid"
date: 2011-04-02 20:51
comments: true
categories: Ruby on Rails, Mongoid, MongoDB
---

[Carrierwave](https://github.com/jnicklas/carrierwave) is an awesome gem for
making file uploads and image processing easy
within Ruby on Rails. I'm currently testing it out with [MongoDB](http://mongodb.org)
and GridFS using
[Mongoid](http://mongoid.org) and it's working almost seamlessly. What took me a days of work with
PHP/Zend Framework now takes me an hour in Rails; just awesome, I think I might
actually go and relax for a couple of hours with the time I've saved =).

The problem I'm having at the moment is that I'm mounting files in an embedded
document; when I delete the parent document, the delete does not bubble down the
the embedded document. This results in the files not been deleted from GridFS
even though the parent document has been destroyed.

This is how I got around the issue. By setting a hook on the after_destroy 
callback method in the parent model.

``` ruby Post.rb
class Post
  include Mongoid::Document
  embeds_many :images, :class_name => "PostImage"

  after_destroy :delete_images!

 # ..
 # ..
 # ..

  def delete_images!
    images.each do |image|
      image.remove_image!
    end
  end
end
```
``` ruby PostImage.rb
class PostImage
  include Mongoid::Document

  attr_accessible :image

  mount_uploader :image, PostImageUploader
  embedded_in :post, :inverse_of => :images

end
```