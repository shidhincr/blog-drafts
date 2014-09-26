# Welcome ES6 !! JavaScript is not fancy anymore

For years, JavaScript was considered as a toy language. It was used for creating interactive web pages and could run only in the browser. But, things changed; JavaScript is used in both server and browser these days. The simplicity of the language made it so popular, and more new developers started adapting for large and complex projects. 

However,still,new developers felt JavaScript is fancy at sometimes. The fanciness is because of some of the known drawbacks in the language itself -- and the workarounds put in place for fixing them. For example, someone from the "C" language background is more familiar to block level scoping, but will have difficulties understanding the lexical scoping in JavaScript. Thus, all these lexical scoping, variable hoisting, closures seems fancy stuff for them.

**TC39**, the committee responsible for ES6 standardization, have seen all these concerns, and ES6 is going to give vast makeover to JavaScript. ES6 has lot of new features added, and existing bad parts fixed. If you don’t know about the JavaScript good vs bad parts, you should definitely check out Douglas Crockford’s book [JavaScript, the Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742)

ES6, the future version, going to give a vast makeover to JavaScript. The **TC39** committee ( responsible for ES6 standardization ) have taken care most of the concerns about JavaScript, and now ES6 is getting lot of new features added, and existing bad parts fixed. If you want to know about the JavaScript good vs bad parts, checkout Douglas Crockford’s book [JavaScript, the Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742).

This post is **not** about complete ES6 feature-set. Here, we'll see some of the areas of JavaScript that looks fancy, and how they're getting improved in ES6.

## ES6, all good parts ?

Again, I am not saying ES6 has only good parts. As of now, most of the ES6 features are not supported by browsers ( as they’re in draft ). Once developers start writing the code more and more, we can clearly see what are the good and bad parts of ES6. 

Currently, we use transpiler tools to compile ES6 code to ES5. There are many tools available, but Google’s [traceur](https://github.com/google/traceur-compiler) is the popular among them.

## 8 fancy things fixed in ES6 

Below are some interesting improvements done in ES6.

**Object.is for better comparison**

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
**Let for block scoping.**

One of the other problem new JavaScript developers face is understanding the lexical scoping. If you’re coming from a language like “C”, you’re more familiar to the block level scoping of variables. But when it comes to JavaScript, there’re not block level scoping. All the variables are hoisted to its containing function ( if there’s any ) else will be part of the global scope. Let’s see the below code: 

```javascript
if(true){
  var a = 10;
  console.log(a); // 10
}
// outside the if block
console.log(a); // a is accessible here also and prints 10
```
The following is a popular example of this scope issue. See below

Assume that we have 10 anchor tags in an html page. We need to have a JavaScript code to alert the index of each anchor tag whenever it’s clicked. Typically, the code might look like this:

```javascript
var anchors = document.getElementsByTagName(“a”);
for(var i=0,len=anchors.length; i<len; i++){
	anchors[i].onclick = function(){
		alert(i);
	};
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
		};
	})(i);
}
```
See how much extra code we need to add to make it work ? Also, this piece of code is unreadable for those are new to JavaScript.

ES6 introduces block scoping in JavaScript using the keyword `let`. If we write our  first example, using `let`:

```javascript
if(true){
  let a = 10;
  console.log(a); // 10
}
// outside the if block
console.log(a) // Reference error: a is not defined
```

`let` also binds the scope to the current block. So in our second example, we use `let` to solve the scoping problem:

```javascript
var anchors = document.getElementsByTagName(“a”);
for(let i=0,len=anchors.length; i<len; i++){
	anchors[i].onclick = function(){
		alert(i);
	}
}
```
The above code should work as expected.

**Multi-line strings and string interpolations.**

Writing multiline strings is not straightforward. We need to use `\n` ( for newline ) whenever we need a line break.

```javascript
var myString = 'Lorem ipsum \ndolor sit amet,\n\n\n consectetur adipisicing\n elit.';
```
The above code lacks readability. ES6 introduces **template strings** for creating multiline strings. In ES6, we can write the above example like this:
```javascript
	var myString = `Lorem ipsum 
    				dolor sit amet,
                    
                    consectetur adipisicing
                    elit.`;
```
So, here, we use "\`" ( backtick ) to create the strings.

Another interesting usecase of the template strings is variable interpolation. In ES5, we cannot do interpolation, but we can achieve similar by replacing the string with regular expressions or by manually appending the variable to the string. For example,

```javascript
// Using + operator 
var name = 'Tony';
var age = 20;
var greeting = 'Hi, I am '+name+' and my age is '+age;
console.log(greeting); // This prints 'Hi I am Tony and my age is 20'

// Using regular expressions
var greeting = 'Hi, I am %name% and my age is %age%'.replace(/%name%/g,name).replace(/%age%/g,age);
console.log(greeting); // This prints 'Hi I am Tony and my age is 20'
```
In ES6, the above code is so much simplified. Same can be written like this:

```javascript
var name = 'Tony';
var age = 20;
var greeting = 'Hi, I am ${name} and my age is ${age}';
console.log(greeting); // This prints 'Hi I am Tony and my age is 20'
```

**Fat Arrow functions for binding `this`**

Most of the new developers get struggled to understand the `this` in JavaScript. The `this` is nothing but the execution context for a function. And for object methods, `this` points to the object holding the method. If the function is executed not as an object method, the `this` will point to the global object ( usually the window object).

`this` can be confusing so many times. Look at the below example:

```javascript
var name = 'Tom';
var obj = {
    name: 'Jerry',
	sayName: function(){
    	console.log( this.name );
    }
};
obj.sayName(); // logs Jerry
var sayName = obj.sayName;
sayName(); // logs Tom
```

When the `sayName` is executed as an object method, `this` was pointing to object itself; but when it's executed as a normal function, `this` was pointing to the global window object.

In ES5, we use either `Function.bind` or `Function.call` or `Function.apply` to fix this kind of problems. All these methods use to dynamically change the `this` ( execution context )  of a function. So we can write it like this:

```javascript
var name = 'Tom';
var obj = {
    name: 'Jerry',
	sayName: function(){
    	console.log( this.name );
    }
};
obj.sayName(); // logs Jerry

// Using call or apply
var sayName = obj.sayName;
sayName.call(obj); // logs Jerry
sayName.apply(obj); // logs Jerry

// Using bind
var sayName = obj.sayName.bind(obj);
sayName(); // logs Jerry
```

ES6 added arrow functions to get rid of the scoping problems. An arrow function will always lexically binded `this` value to the holding object. So the above code can be written in ES6 like this:

```javascript
var name = 'Tom';
var obj = {
    name: 'Jerry',
	sayName: => {
    	console.log( this.name );
    }
};
obj.sayName(); // logs Jerry
var sayName = obj.sayName;
sayName(); // logs Jerry
```
**Note:** _Since the arrow function is already bound its execution context, we cannot apply .bind(), .call() or .apply() methods on it again._

**Destructuring**

One of the hardest thing in ES5 is destructuring. Destructing is the process of assigning the property values of an object to local variable. For example, in ES5, we do like this:

```javascript
	var myGlobalConfig = {
    	apiUrl: 'www.google.com/api',
        data1: 'some value',
        data2: 'another value',
        methodType: 'POST'
        // ... etc
    };
    
    // and in one of our function
    
    function makeAjaxRequest(config){
    	var url = config.url;
        var method = config.methodType;
        var data = config.data2;
        $.ajax(url, method, data );
    }
    
    // call makeAjaxRequest
    makeAjaxRequest( myGlobalConfig );
```

In the above code, whenever a function requires arguments as multiple parameters, we need to extract values from the our config object and pass them as parameters. That is, seriously, a lot of code.

ES6 allows direct destructing assignments. So we can write the above example in a simple way, like this:

```javascript
	var myGlobalConfig = {
    	apiUrl: 'www.google.com/api',
        data1: 'some value',
        data2: 'another value',
        methodType: 'POST'
        // ... etc
    };
    
    // and in one of our function
    
    function makeAjaxRequest(config){
    	var { url, methodType, data2 } = config;
        $.ajax(url, methodType, data2 );
    }
    
    // call makeAjaxRequest
    makeAjaxRequest( myGlobalConfig );
```

**Default Arguments Values for Functions**

One of the best feature in ES6 is default arguments. As of now, we use the `||` to have default values for the function parameters. See the below code:

```javascript
	var myFunction = function(a, b, c){
    	a = a || 10;
        b = b || 5;
        c = c || 8;
        return a*b*c;
    };
```
Here is the same code will be written in ES6:

```javascript
	var myFunction = function(a=10, b=5, c=8){
        return a*b*c;
    };
```
**Object method shorthands**

In JavaScript, one of the common design pattern while for objects is the revealing module pattern. In this pattern, all the public method/property of an object will have its own private counterpart. For example,

```javascript
	var myObject = (function(){
    	var sayName = function(){
        	console.log('this is sayname function');
        };
        var greet = 'This is a greeting';
        return {
        	greet: greet,
        	sayName: sayName
        }
    })();
```
The above pattern is called **Revealing module pattern**. ES6 simplified this much better by eliminating the column part. Thus, in ES6, we can write the above code like this:

```javascript
	var myObject = (function(){
    	var sayName = function(){
        	console.log('this is sayname function');
        };
		var greet = 'This is a greeting';
        return {
        	greet,
        	sayName
        }
    })();
```

**The super keyword for invoking super class methods.**

JavaScript supports object oriented programming. But, inheritance is tricky in JavaScript, as it's not support natively. JavaScript even has the `super` keyword, however, it's not functional.

Most of the JavaScript frameworks, those who implemented inheritance, have a pattern like this:

```javascript
	var myBaseObj = {
    	sayName: function(){
        	// .. do something
        };
    };
    
    var mySubObj = Framework.extend(myBaseObj, {
    	sayName: function(){
        	this._super.apply(this,arguments);
            // .. do something else
        }
    })
```
These framework used `_super` ( or sometimes `uber` ) to invoke the parent method. This is because, `super` was a keyword in JavaScript, and it's not allowed to use it as an identifier or method. 

Now, the time has come; We have `super` implemented in ES6, and see how the inheritance can be done:

```javascript
	var myBaseObj = {
    	sayName: function(){
        	// .. do something
        };
    };
    var mySubObj = {
    	__proto__: myBaseObj,
    	sayName: function(){
        	super.sayName();
            // .. do something else
        }
    })
```

Again, all these are just a small part of ES6 featureset. There are so many interesting features like Promises, Classes, Generator and Iterators ..etc. 

## Summary

ES6 is the most promising version of JavaScript. It has so many features, those,  we were waiting for years. Definitely, ES6 will help writing more modular and less quirky code in JavaScript.

Here in this article, we have seen the problems with the current version of JavaScript, and how ES6 improved to fix them and workarounds. Now, the entire ES6 feature sets are beyond the scope of this post, for that you can also checkout these awesome resources.

- https://github.com/lukehoban/es6features
- https://github.com/ericdouglas/ES6-Learning
- http://espadrine.github.io/New-In-A-Spec/es6/
- http://tc39wiki.calculist.org/es6/
