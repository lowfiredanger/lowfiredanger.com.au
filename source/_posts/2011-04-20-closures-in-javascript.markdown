---
layout: post
title: "Closures in javascript"
date: 2011-04-20 21:10
comments: true
categories: Javascript
author: Sonny Mai
---

To understand closures, you should first understand that functions in javascript can be used as variables as below.

Functions as variables
----------------------

Within the Javascript language, functions are treated as variables. This means that you can pass functions around like variables. which lets you doing something like this:

``` javascript
	function createUselessFunction(value){
		return function(){
			alert(value);
		};
	}

	var newFunction = createUselessFunction('cat');

	newFunction(); //Alerts 'cat'
	
	//Alternative syntax
	createUselessFunction('dog')(); //Alerts 'dog'
```

Closures
--------

Closures are basicly functions that enclose variables. Here is an example.

``` javascript
	function anotherUselessFunction(value){
		var localVariable = "I am local";
		
		return function(){
			alert(value + ' ' + localVariable);
		}
	}
	
	var uselessFunction = anotherUselessFunction('WOW!');
```
	
What happens when we execute uselessFunction()? Would localVariable be accessible from function returned by uselessFunction()? It turns out that it is accessible.

	uselessFunction(); //Alerts 'WOW! I am Local'
	
So we see that javascript "closes" in local variables and allows returned functions to access these variables. An example use for this behaviour is described below. This example shows how we can create a custom multiplier.
	
``` javascript
	function multiplier(amount){
		return function(number){
			alert(amount * number);
		};
	}
	
	var timesFive = multiplier(5);
	
	// 5 x 3
	timesFive(3); //Alerts 15
	// 5 x 12
	timesFive(12); //Alerts 60
```
Notice how 5 gets stored inside the timesFive function and we can reuse the timesFive variable as a function multiple times?

Javascript is whacky and fun!
	