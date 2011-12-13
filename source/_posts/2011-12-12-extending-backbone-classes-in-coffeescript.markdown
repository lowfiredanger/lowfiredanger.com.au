---
layout: post
title: "Extending Backbone.js classes in CoffeeScript"
date: 2011-12-12 22:10
comments: true
categories: Javascript, Backbone.js
author: Sonny Mai
---

Here's a very quick how-to on extending backbone classes and over riding their methods in coffeescript. You can even call super; that will let you call the original method once you're complete.

``` coffeescript greeter.js
class Greeter extends Backbone.View  
	initialize: () ->
  	# Initialize things here

	greet: ->
		alert 'Hello'
```

``` coffeescript multi_lingal_greeter.js
class MultiLingalGreeter extends Greeter
	initialize: () ->
	# Initialize things here

	greet: ->
		alert 'Bonjour'
		super
```

And now we can create a new instance of the ```MultiLingalGreeter``` class then call the greet method. We will get two alert boxes, the first one will say Bonjour, followed by Hello. This happens because ```super``` is being called, which calls the original method of the class

``` javascript
greeter = new MultiLingalGreeter();
greeter.greet() // Alerts 'Bonjour' followed by 'Hello'
```

What happens when we create another class that extends the ```MultiLingalGreeter```? Will calling super inside ```greet()``` execute the Greeter class directly or only the method inside ```MultiLingalGreeter```?

``` coffeescript drunk_greeter.js
class DrunkGreeter extends MultiLingalGreeter
	initialize: () ->
	# Initialize things here

	greet: ->
		alert 'Aarhohhoah *spew*'
		super
```

Turns out, it'll only call the method inside ```MultiLingalGreeter```. The ```super``` method inside ```MultiLingalGreeter``` will then call the original ```Greeter``` class.
So you'll get alerts in the following order:

1. Aarhohhoah \*spew\*
2. Bonjour (called from the ```super``` inside ```DrunkGreeter```)
3. Hello (called from the ```super``` inside ```MultiLingalGreeter```)

Conclusion: Backbone.js + Coffeescript is sexy isn't it?
