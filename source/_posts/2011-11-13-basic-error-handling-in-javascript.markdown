---
layout: post
title: "Basic error handling in javascript"
date: 2011-11-13 21:59
comments: true
categories: 
published: false
---

I've noticed error handling is often an afterthought in javascript I've seen (I admit that I'm a little guilty myself, but hey, at least I'm aware right?!). Good error handling can make your javascript more easier to debug and less brittle.

Here are some basics to javascript error handling.

## Selective catching of errors

Here we have a function that

``` javascript

var invalid_input_error = new Error("Invalid string input");

function age_input(){
	var age = prompt("How many cats do you own?", "");
	if (isNaN(age)){
		throw invalid_input_error;
	}

	alert("You have " + age + " cats!? That's fabtastic");
}
```