---
layout: post
title: "lightModal - a lightweight lightbox/modal in coffeescript"
date: 2011-11-12 22:35
comments: true
author: Sonny Mai
categories: 
---

I recently made a really lightweight modal box to use on one of our projects [LessPlan](http://lessplan.com "Easily manage Lesson plans for teachers"). There was a need to have a instance of tinyMCE within a modal/lightbox when creating a lesson plan.

What I found was most existing modal/lightbox plugins was that they were incompatible with tinyMCE because they cloned the contents of a specified div before placing it into the actual lightbox container.

LightModal does away with the cloning and makes the content itself turn into a lightbox, therefore throwing away the need to clone the html.

It's written in CoffeeScript as a jquery plugin and includes tests written with Jasmine BDD testing framework. Released under the MIT licence.

[Get the source and demo here](/opensource/lightModal)


