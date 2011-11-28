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

## Throwing and catching basic errors

``` javascript
function
```

## Selective catching of errors

Here we have a function that

``` javascript

var invalid_cats_error = new Error("Invalid cat input");

function cats_input(){
	var number_of_cats = prompt("How many cats do you own?", "");
	if ( isNaN(number_of_cats) ){
		throw invalid_input_error;
	}

	var cat_name = prompt("");

	alert("You have " + number_of_cats + " cats!? That's fabtastic");
}

// Call the function
try {
	
} catch (e) {
	if ( e != invalid_cats_error )
   		alert("You didn't enter the a number =(");
}
cats_input();
```