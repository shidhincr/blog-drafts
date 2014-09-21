Welcome ES6 !! JavaScript is not fancy anymore

Introduction

Point: Javascript has lot of quirks; Only seasoned developers could able to find them easily and fix it; Javascript has good parts and bad parts ; Douglus crockford has a book about good parts; ES6, would be a dream thing and life saver for most of these; 

Point: Not going to talk about all the ES6 features; but comparing some of the code in ES5 and how that can be done in ES6, in right way.
ES6, all good parts

I am not saying ES6 has only good parts; I am not aware of any bad parts as of now. This is because, ES6 is still not ready to be production version; There are tools like traceur we can use to convert our ES6 code to ES5, so that the current browsers can execute it. 

The feature set is awesome.. [Links to ES6 official draft from ecmascript ]

We’ll see some of the basic set is used to solve the current JavaScript quirks. 

7 fancy things fixed in ES6 

Object.is for better comparison
=== is better always for type coercion and comparison
But fails for NaN. Object.is will work for NaN

Let for block scoping. ( show the problem of for loop alert button solved in ES5 using closures and same can be done in ES6 without closures ) ( refer nicholas articles or try it in firefox )
No block scopes inside for loops
For example, alerting inside a for loop

Multi-line strings and string interpolations.
Writing multi line strings in JavaScript was a pain
using ‘+’ operator for multiline strings
using \ operator for mult line strings
using Array join for more readability

Fat Arrow functions for binding ‘this’
One of the scariest for new developes is ‘this’ keyword.
Simple example of attaching an event handler to and accessing ‘this’ inside that
Javascript developers fix this problem using that=this; or self=this; ..etc OR even with ES5, using the function .bind() will help to fix this problem
Fat arrows will make sure that the ‘this’ will always points to the current object. 
Won’t be able to use .bind(), .call() or .apply() functions to change the context of the execution of the fat arrow functions.

Destructuring 

Refer one of the code from Namshi, ( I guess in connect where I take the oAuth clientId details from configurations )
Destructing helps to directly assign values to variables in local scope

Default Arguments and Object method shorthands

No more using the ‘||’ operator for default arguents ( explain this )
No need of the revealing module patterns. We can skip the column part; JavaScript engine will figure it out

The super keyword for invoking super class methods.

Inheritance is one of the key part of  OOP.
Doing inheritance is difficult in JavaScript. and mostly in most of the frameworks implemented inheritance will have a method like this:
subClass._super.apply(this, arguments); or subClass.uber.apply(this,arguments)
Here we have the super keyword to the rescue. ‘super’ will point to the parent object i this case:
```javascript
var child = {
      // __proto__
      __proto__: parent,
      eat: function(){
      	super.eat();
      }
};
```
Apart from all these, ES6 added lot of new features, like Promises, Classes, Generator and Iterators ..etc. 

Summary

ES6 is not ready to use; But it definitely going to change the future of JavaScript. The feature set of ES6 is really awesome. ES6 will help us to write more modular and less quirky codes. 

ES6 features are not ending here.. You can read these awesome resources to have a grasp of the upcoming ES6 features.

https://github.com/lukehoban/es6features
https://github.com/ericdouglas/ES6-Learning
http://espadrine.github.io/New-In-A-Spec/es6/ 
