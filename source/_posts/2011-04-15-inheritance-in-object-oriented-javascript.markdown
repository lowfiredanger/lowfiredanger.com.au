---
layout: post
title: "Inheritance in Object Oriented Javascript"
date: 2011-04-15 21:21
comments: true
categories: Javascript
Author: Sonny Mai
---

Writing maintainable and reusable code in javascript is difficult when writing it functionally, especially in larger applications. Writing object oriented javascript is a useful skill you should learn if you plan to spend a large portion of your time developing the front-end of web applications.

In order to make objects in javascript reusable, child classes should be able to inherit methods and properties of their parent class. I'll be going though some concepts of "classical" inheritance; as there are a few ways to achieve inheritance in javascript. This includes:

- Prototypal
- Using Mix-ins (Great if you have a ruby background)
- Borrowing methods using call or apply

I'll discuss these methods in a future article. Theres no "more" correct method for inheritance, I believe it's a matter of opinion and comfort. For now I'll just go through some concepts of classical inheritance; because most people are more familiar with classical inheritance from languages such as java, php, C++ etc.

Below is some code to demonstrate the basics of creating a class and instantiating that class.

``` javascript
	//Pet class
	var Pet = function(name){
		this.name = name || "Snowy";

		this.move = function(){
			return alert(this.name + " is walking");
		}
	}
	
	//Creating an instance of Pet
	var myBird = new Pet("Tweety");
	myBird.move(); //Alerts 'Tweety is walking'
```
	
In the above example, we define the class "Pet" (note the var name is capitalised as a convention to indicate this is a constructor function (Constructor functions are basically any function that you can create instances of, i.e. classes)). We also give the Pet class an instance variable "name" (the name of the pet). A instance method is also given to the the Pet class "move".

We then create a new instance of Pet for our bird named "Tweety". We then call the "move" method, which alerts us with "Tweety is walking". So that sounds about right, except birds mostly don't walk, they fly. So we should extend the Pet class to accommodate for pet birds.

``` javascript
	var Pet = function(name){
		this.name = name || "Snowy";

		this.move = function(){
			return alert(this.name + " is walking");
		}
	}

	//Create an placeholder Class
	function Bird(){};

	//Inherit the Pet class into the Bird class
	Bird.prototype = new Pet();
	//Over-ride the move function using prototype
	Bird.prototype.move = function(){
		return alert(this.name + " is flying");
	}

	var myBird = new Bird('Tweety');
	myBird.move(); //Alerts 'Snowy is flying'
```	

That looks all great and seems to work well; except it outputs "Snowy is flying" instead of "Tweety is flying"! What is happening here? It turns out the child class "Bird" does not pass the constructor parameters to the parent. So that is not a really ideal solution to this problem. We need to pass in the constructor object using apply().

``` javascript
	var Pet = function(name){
		this.name = name || "Snowy";
		
		this.move = function(){
			return alert(this.name + " is walking");
		}
	}
	
	function Bird(name){
		Pet.apply(this, arguments);
	};
	
	Bird.prototype = new Pet();
	Bird.prototype.move = function(){
		return alert(this.name + " is flying");
	}
	
	var myBird = new Bird('Tweety');
	myBird.move(); //Alerts 'Tweety is walking'
```

Now we got "Tweety" appearing in the move() method, but now the method is coming from the original Class; so instead of "Tweety is flying", we get "Tweety is walking". It turns out that we the method first looks inside of the parent class for the method before visiting the prototype.

``` javascript
	var Pet = function(name){
		this.name = name || "Snowy";
	}
	
	Pet.prototype.move = function(){
		return alert(this.name + " is walking");
	}
	
	function Bird(name){
		Pet.apply(this, arguments);
	};
	
	Bird.prototype = new Pet();
	Bird.prototype.move = function(){
		return alert(this.name + " is flying");
	}
	
	var myBird = new Bird('tweety');
	myBird.move(); //Alerts 'Tweety is flying'
```

We have moved the method of move() outside of Pet into a prototype function. This allows the method to be over-ridden by the Bird class.

Thats all for now, hope that was useful!