# Welcome ES6 !! JavaScript is not fancy anymore

For years, JavaScript was considered to be a toy language. But, things changed, and JavaScript is one of the popular and powerful language in the world. The simplicity of the language made it so popular, however, new developers trying to learn JavaScript feel that it’s fancy sometimes. 

The fanciness is because of some of the known problems with the language itself -- and the workarounds for fixing those. For example, a developer coming from C based languages will have problems with JavaScript variable scopes and hoisting (  as JavaScript doesn’t have block scoping ), and he might feel the lexical scoping in JavaScript is fancy.

**TC39**, the committee responsible for ES6 standardization, have seen all these concerns, and ES6 is going to give vast makeover to JavaScript. ES6 has lot of new features added, and existing bad parts fixed. If you don’t know about the JavaScript good vs bad parts, you should definitely check out Douglas Crockford’s book [JavaScript, the Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742)

In this post, we’re not going to discuss about ES6 feature sets. Here, we’ll see some of the fancy JavaScript code we write in ES5 ( the current version ) and how they’re getting improved in ES6.

## ES6, all good parts ?

Again, I am not saying ES6 has only good parts. As of now, most of the ES6 features are not supported by browsers ( as they’re in draft ). Once developers start writing the code more and more, we can clearly see what are the good and bad parts of ES6. 

Currently, we use transpiler tools to compile ES6 code to ES5. There are many tools available, but Google’s [traceur](https://github.com/google/traceur-compiler) is the popular among them.


## 7 fancy things fixed in ES6 

- **Object.is for better comparison**

New developers who learn JavaScript often get stumbled on the usage of `==` and `===`.  The `===` is a strict comparison operator where it checks the type of the operands too. For example, in the below code:

```javascript
“0” == 0  // true

but

“0” === 0 // false
```

It’s always recommended to use `===` operator. However, `NaN`  is an exceptional case even if we use the `===` for comparing. That means, 

```javascript
NaN == NaN  // false
NaN === NaN  // false
```

`Object.is` an attempt to have a better comparison method. It more or less similar to the `===` operator, except it does the proper comparison for NaN also.

```javascript
Object.is(0 ,”0”) // false
Object.is(0 ,0) // true
Object.is(NaN, NaN) // true
```
- **Let for block scoping.**

One of the other problem new JavaScript developers face is understanding the lexical scoping. If you’re coming from a language like “C”, you’re more familiar to the block level scoping of variables. But when it comes to JavaScript, there’re not block level scoping. All the variables are hoisted to its containing function ( if there’s any ) else will be part of the global scope. Let’s see the below code: 

```javascript
if(true){
  var a =10
  console.log(a) // 10
}
// outside the if block
console.log(a) // a is accessible here also and prints 10
```

The following is a popular example of this scope issue. See below

Assume that we have 10 anchor tags in an html page. We need to have a JavaScript code to alert the index of each anchor tag whenever it’s clicked. Typically, the code might look like this:

```javascript
var anchors = document.getElementsByTagName(“a”);
for(var i=0,len=anchors.length; i<len; i++){
	anchors[i].onclick = function(){
		alert(i);
	}
}
```

The above code doesn’t work as expected. Whenever we click on any of the anchor tag, we’re going to get the last value of `i`. Here, we’ll get always 10 alerted. 

To  workaround this kind of situations, in ES5, we use closures. Using closures, we can bind the right value of `i` to the onclick handler. See the code below:

```javascript
var anchors = document.getElementsByTagName(“a”);
for(var i=0,len=anchors.length; i<len; i++){
	anchors[i].onclick = (function(){
		return function(){
			alert(i);
		}
	})(i)
}
```

See how much extra code we need to add to make it work ? Also, this kind of code is unreadable for those are new to JavaScript.

ES6 introduces block scoping in JavaScript using the keyword “**let**”. If we write our  first example, using “**let**”:

```javascript
if(true){
  let a =10
  console.log(a) // 10
}
// outside the if block
console.log(a) // Reference error: a is not defined
```

“**let**” also binds the scope to the current block. So in our second example, we can just use let to solve the scoping problem:

```javascript
var anchors = document.getElementsByTagName(“a”);
for(let i=0,len=anchors.length; i<len; i++){
	anchors[i].onclick = function(){
		alert(i);
	}
}
```
The above code should work as expected.

 
- **Multi-line strings and string interpolations.**
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
var child = {
    // __proto__
    __proto__: parent,
	eat: function(){
	super.eat();
}
};

Apart from all these, ES6 added lot of new features, like Promises, Classes, Generator and Iterators ..etc. 

Summary

ES6 is one of promising version of JavaScript. It has lot of features those developers were aspiring for years. Definitely, ES6 will help writing more modular and less quirky code in JavaScript.

Here in this article, we have seen the problems with the current version of JavaScript, and how ES6 improved to fix them and workarounds. Now, the entire ES6 feature sets are beyond the scope of this post, for that you can also checkout these awesome resources.

https://github.com/lukehoban/es6features
https://github.com/ericdouglas/ES6-Learning
http://espadrine.github.io/New-In-A-Spec/es6/ 
