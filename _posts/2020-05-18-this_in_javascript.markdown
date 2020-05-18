---
layout: post
title:      "This in JavaScript"
date:       2020-05-18 15:50:57 +0000
permalink:  this_in_javascript
---


Coming info JavaScript the `this` keyword was confusing and how if performed in functions. The `this` keyword behaves differently in JavaScript than other languages, and I found myself using the `'use strict'` for `this` when learning functions. It may be different each time the function is called in `non-strict` mode. In non-strict mode the `this` refers to an object, strict mode it can be any value.

When a function executes it gets the `this` property.
Using this in a function can be used to invoke properties within a function. 
```
     let user = {
		   firstName :"Fede",
			 lastName :"Serai"
			 
			 fullName: function(){
			   console.log(this.firstNAme + " " + this.lastName);
			 }
		 }
		 
		 user.fullName();
```

Since the `this` keyword is used inside the fullName method and is defined on the user object, `this` will have the value of the user object that will invoke fullName. 

The `this` keyword in the example above shows that `this` is not assigned a value until an object invokes the function where this is defined.
