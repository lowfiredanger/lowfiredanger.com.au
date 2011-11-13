---
layout: post
title: "Backbone.js mixins"
date: 2011-11-14 00:49
comments: true
categories: Javascript, Backbone.js
author: Sonny Mai
---

[Backbone.js](http://documentcloud.github.com/backbone/) is a great javascript mvc framework to create frontend js heavy applications.

What happens when there you start building your backbone.js app but find that there is substantial boilerplate code that you want to reuse?

One cool feature, that's not necessarily a part of backbone.js is mixins. If you're familiar with Ruby, then it should be a familiar concept. Mixins are basically a way to inherit another class, or module and be able to use the inherited class's functions/methods.

To create a mixin in backbone, you use underscores nifty ```_.extend()``` method to allow an object to inherit some other objects methods.

Take the following silly example. If you wanted to reuse the functions in the ComplexMaths object, how would you do it with ```_.extend()```?

``` javascript complex_maths.js
var ComplexMaths = {
	addition: function(number1, number2){
		return number1 + number2;
	}
}
```

Simple

``` javascript calculator.js

Calculator = Backbone.View.extend({
  initialize: function() {
    _.bindAll(this, "blah...");
  }

  // ..
  // ..
  // ..

});

// Mixin here
_.extend(Calculator.prototype, ComplexMaths);

```

The final line of the script above, underscore accepts the destination object ```Calculator.prototype``` and duplicates the properties inside source object ```ComplexMaths``` into ```Calculator.prototype```.

Now you have the power to create whole libraries of reusable useful stuff!