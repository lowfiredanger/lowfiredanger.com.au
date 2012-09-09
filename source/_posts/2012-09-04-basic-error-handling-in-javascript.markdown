---
layout: post
title: 'Basic error handling in javascript'
date: 2012-09-04 21:59
comments: true
categories: Javascript
published: true
author: Sonny Mai
---

I've noticed error handling is often an afterthought in javascript I've seen. Good error handling can make your javascript more easier to debug, more efficient and more robust.


## A less than optimal way to catch errors

A less optimal way to catch errors and notify the caller is by returning a special value such as undefined, or a boolean or whatever. Below is an example.

``` javascript
var doubleYourAge = function(age){
	if(age < -1 || isNAN(age)){
		return undefined;
	}else{
		return age * 2;
	}
};

// Call the function
if(typeof doubleYourAge(-18) === 'undefined'){
	alert('Your input is invalid')
}

```

This works great, but it means that everytime you call ```doubleYourAge```, you are forced to perform a check. This can be inefficient if you're calling the function multiple times in your scripts.

## Throwing and catching basic errors

A better way, but still not the best, is to throw an error.

``` javascript

var cats_input = function(){
	var number_of_cats = prompt('How many cats do you own?');
	if (isNaN(number_of_cats) || number_of_cats < 0){
		throw 'Not a valid number';
	}

	alert("You have " + number_of_cats + " cats! That's fantastic");
}

// Call the function
try {
	cats_input();
} catch (e) {
	alert('We caught an error: ' + e);
}

```

The above code is better than the first example, it only needs to run the error handling code if an error actually occurs, and no checking needs to be done everytime the funciton is called. Depending on your use-case, you might want to catch specific erros and conditions. This is where selective catching of errors is useful.

## Selective catching of errors

The script below does the same thing as above, only this time, we instantiate Error objects which allows us to:
- throw specific errors
- catch and handle each error condition individually.

``` javascript

var not_a_number_error = new Error('Cat input is not a number');
var below_zero_error = new Error('Cat input is smaller than zero');

var cats_input = function(){
	var number_of_cats = prompt('How many cats do you own?');
	if (isNaN(number_of_cats)){
		throw not_a_number_error;
	}
	if (number_of_cats < 0){
		throw below_zero_error;
	}

	alert("You have " + number_of_cats + " cats! That's fantastic");
}

// Call the function
try {
	cats_input();
} catch (e) {
	if ( e != invalid_cats_error ){
   		alert("You didn't enter the a number");
   	}else if ( e != invalid_cats_error ){
   		alert('Your number is less than zero');
   	}
}
```

There you go, simple, easy error handling with javascript.