# JavaScript Learning Notes
- - - - -
## Execution Contexts and Lexical Environments


- **this**
   In the inspector( in the navigator ) under the console window, we can type 'this'         to see all the global object. 

- **console.log()**

- - - - -
## Types and Operators
### Type
- **undefined** - key word
    the variable is created in the memery but has no value.

- **null**
- **boolean**
- **number**
- **String** is primitive type in JavaScript
- **symbol** used in ES6

### Operator ' == ' and ' === '
- **' a == b  '**  - Equality - If  a and b have the same value
- **' a === b '** - Strict Equality - If a and b have the same value and if a and b have the same type

### Existence and Boolean
```JavaScript
    Boolean(undefined); // false
    Boolean(null); // false
    Boolean( "" ); // false
```
Usage: 
```JavaScript
var a;
if ( a ){ // if a has value
}
```
- - - - -
## Objects and Functions
### JSON ( JavaScript Object Notation )
```JavaScript
var jsonString = JSON.stringify( yourObject ); // build-in method to convert Object to JSON
```
```JavaScript
var yourObject = JSON.parse( jsonString ); // build-in method to convert JSON string to an Object
```

### Functions are Objects
```JavaScript
function greet() {
	console.log('hi');
}
greet.language = 'english';
console.log(greet.language);  // in console: english
```

### Values and References
For **primative value**:
```JavaScript
var a = 1; // or any other primative value ( boolean, string .... )
var b = a; //  a and b pointed two different value
b = 2;
console.log('a = ' + a);
console.log('b = ' + b);
// output is : a = 1  b = 2
```
For **Object**:
```JavaScript
var a = { number: 1};
var b = a;
b.number = 2;
console.log('a.number = ' + a.number);
console.log('b.number = ' + b.number);
// output is : a.number = 2   b.number = 2
```
In order to create a new memory space for Object :
```JavaScript
var a = { number: 1};
var b = a;  // a already exist in memory, so just point b to a ( they are pointed to the same object )
b.number = 2;
a = {number: 1}; // create a new object in the memory, than point a to this new object
console.log('a.number = ' + a.number);
console.log('b.number = ' + b.number);
```
### " this "
**in the function**
```JavaScript
function a() {
    console.log(this); // here, 'this' will show the global variables
}
```
**in the object**
```JavaScript
var c = {
    name: 'The c object',
    log: function() {
        this.name = 'Updated c object!'; // it will change the name property in the 'c'
        console.log(this); // it will show object 'c'
    }
}
c.log(); 
```
**in the function of a function of an object**
```JavaScript
var c = {
	name: 'the c object',
	log: function() {
		this.name = 'Updated c object';
		 console.log(this);
		 var setname = function(newName) {
		 	this.name = newName; // 'this' will create a new variable 'name'  to the global object instead of changing the 'name' property in object 'c'
		 }
		 setname('Updated again! The c object');
		 console.log(this);
	}
};
```
this is not like other languages. So, how to solve this problem?
```JavaScript
var c = {
	name: 'the c object',
	log: function() {
		var self = this;  // create a variabel point to the object 'c'
		self.name = 'Updated c object';
		 console.log(self);
		 var setname = function(newName) {
		 	self.name = newName; // use 'self' that we created instead of 'this'
		 }
		 setname('Updated again! The c object');
		 console.log(self);
	}
};
```
### Array
```JavaScript
var arr = [
	1,
	false,
	{
		name: 'william',
		address: 'my address'
	},
	function(name) {
		var greeting = 'hello ';
		console.log(greeting + name);
	},
	'hello'
];
arr[3](arr[2].name); 
```
### Arguments
```JavaScript
function testFunction(firstname = 'wang', lastname = 'xi' , language = 'cn'){ //set the defaul value 
}
```
But this method is not supported by some broswers. So we can use another method :
```JavaScript
function testFunction(firstname, lastname, language) {
    firstname = firstname || 'wang';
    lastname = lastname || 'xi';
    language = language || 'cn';
}
```
We can output all the value that parameter have passed use key word 'arguments' :
```JavaScript
function testFunction(firstname, lastname, language) {
    console.log(arguments);
    if(arguments.length === 0){// if there is no parameters passed
        console.log('Missing parameters');
    }else {
        console.log('arg 0 : ' + arguments[0]); // use [] to chose which parameter to print to console
    }
    
}
```
### IIFE ( Immediately Invoked Functions Expressions )
Advantage : won't be effected by the global variables.
```JavaScript
(function(name){
    var greeting = 'My name is: ';
    console.log( greeting + name);
    }('William'));
```

### Closures
```JavaScript
function greet(whattosay) {
	return function(name) {
		console.log(whattosay + ' ' + name);
	}
};
var sayHi = greet('Hi');
sayHi('William');  //it will output 'Hi William', it can get the value of the 'whattosay' which we gave it earlier, event though the function greet() is nolonger existe in the execution stack.
```
**Example:**
```JavaScript
function buildFunctions() {
	var arr = []; 
	for (var i = 0; i < 3; i++ ){
		arr.push(
				function() {
					console.log(i);
				}
			);
	}
	return arr;
}
var fs = buildFunctions();
fs[0]();
fs[1]();
fs[2]();
```
We expected the console shows 0 1 2.

But it shows 3 3 3. How to resolve this problem? We can use closures:
```JavaScript
function buildFunctions2() {
	var arr = []; 
	for (var i = 0; i < 3; i++ ){
		arr.push(
				(function(j) {
					return function() {
						console.log(j);
					}
				}(i))
		);
	}
	return arr;
}
var fs2 = buildFunctions2();
fs2[0]();
fs2[1]();
fs2[2]();
```
### Callback
Callback function is a function you give to another function, to be run when the other function is finished.
```JavaScript
function sayHiLater() {
	var greeting = 'Hi';
	setTimeout( function() { // this is the callback function
		console.log(greeting);
	}, 3000);
}
sayHiLater();
```
Another example:
```JavaScript
function tellMeWhenDone(callback) {
	//some code here
	callback();
}
tellMeWhenDone(function (){
	console.log('I am done');
});
tellMeWhenDone( function (){
	alert('I am done!');
});
```
### call() , apply(), bind()
**bind()**
Make a new copy
```JavaScript
var person = {
	firstname: 'wang',
	lastname: 'xi',
	getFullName: function() {
		var fullname = this.firstname + ' ' + this.lastname;
		return fullname;
	}
};

var logName = function(lang1, lang2) {
	console.log('Logged: ' + this.getFullName());
}

var logPersonName = logName.bind(person); //bind(person) makes keyword 'this' in the 'logName' pointed to the 'person' object

logPersonName(); //console shows: 'Logged: wang xi'
```
**call() and apply()**
The differences between these two method is apply() needs to pass a array instead of singal values.
```JavaScript
logName.call(person , 'arg1', 'arg2');
logName.apply(person,[ 'arg1' , 'arg2' ]);
```
Another example:
```JavaScript
var person = {
	firstname: 'wang',
	lastname: 'xi',
	getFullName: function() {
		var fullname = this.firstname + ' ' + this.lastname;
		return fullname;
	}
};

var person2 = {
	firstname: 'William',
	lastname: 'Wang'
};

var output = person.getFullName.apply(person2);
console.log(output); // console will show: William Wang
```
Another example of bind():
```JavaScript
function multiply(a,b) {
	return a*b;
}

var multipleByTwo = multiply.bind(this,2); // it will set 'a' always = 2
console.log(multipleByTwo(4)); // console shows: 8
```
### Functional Programming
```JavaScript
function mapForEach(arr, fn){
	var newArr = [];
	for(var i = 0; i < arr.length; i++){
		newArr.push(
			fn(arr[i])
			)
	}
	return newArr;
}

var arr1 = [1,2,3];

var arr2 = mapForEach(arr1, function(item){
	return item * 2;
});
var arr3 = mapForEach(arr1, function(item){
	return item > 2;
});

console.log(arr2); // [2,4,6]
console.log(arr3); // [false, false, true]
```
Example with bind()
```JavaScript
function mapForEach(arr, fn){
	var newArr = [];
	for(var i = 0; i < arr.length; i++){
		newArr.push(
			fn(arr[i])
			)
	}
	return newArr;
}

var arr1 = [1,2,3];

var checkPastLimit = function(limiter, item) {
	return item > limiter;
};

var arr4 = mapForEach(arr1, checkPastLimit.bind(this, 1));
console.log(arr4); // [false, true, true]
```
**checkPastLimit.bind(this,1):** it make a copy of function checkPastLimit and set his first parameter ( limiter ) to 1.
- - - - -
##Opensources to learn
- **underscore.js**
- **lodash.js**
- **moment.js**
---

##Object-Oriented JavaScript
###Inheritance
The prototype of the Object.
```JavaScript
__proto__
```

Use the method ' **_.extend()** ' in the library **underscore.js** to inherit.
---

## Building Objects
### prototype
'prototype' is the build-in property for different object  

### Diffrent way to build/construct objects
Functions are objects in JavaScript  
Key word ' **New** '
```JavaScript
function Person(firstname, lastName) {
	this.firstname = firstname;
	this.lastName = lastName;
}

Person.prototype.getFullName = function() {
	return this.firstname + ' ' + this.lastName;
}; // it's better to put the function into the 'prototype'(instead of write it in the 'Person') , so when the new instances of the 'Person' are created, the function 'getFullName' won't be recreated in the memory many times, it will have just one copy in the memory. For performentce purpose.

var william = new Person('William', 'Wang');
console.log(william); // Person {firstname: "William", lastName: "Wang"}
```

### The dangers to use build-in function constructors
```JavaScript
var a = 3;  // a is the primative 
var b = new Number(3); // b is an object
var c = Number('3');

console.log(a == b); // true
console.log(a === b); // false

console.log(a == c); //true
console.log(a ===c); //true
```

### Array and for-in
In order to loop an array, do not use ' for-in ' loop, use standered ' for ' loop

### Object.creat()  ( pure prototypal inheritance )
```JavaScript
var person = {
	firstname: 'Default',
	lastname: 'Default',
	greet: function() {
		return 'Hi ' + this.firstname;
	}
};

var william = Object.create(person); // it will creat a empty object with the prototype pointing to the ' person '
william.firstname = 'William';
william.lastname = 'Wang';
console.log(william.greet()); // Hi William
```
**Polyfill**
```JavaScript
if (!Object.create) {
	Object.create = function (o) {
		if(arguments.length > 1) {
			throw new Error('Object.create implementation only accepts the first parameter');
		}
		function F(){}
		F.prototype = o;
		return new F();
	};
}
```

### ES6 And Classes
```JavaScript
class Person {
	constructor(firstname, lastname) {
		this.firstname = firstname;
		this.lastname = lastname;
	}

	greet() {
		return 'Hi ' + this.firstname;
	}
}

var william = new Person('William', 'Wang');
console.log(william.greet());// Hi William
```

**Key word ' extends ' **
```JavaScript
class InfomalPerson extends Person {
	constructor(firstname, lastname){
		super(firstname, lastname);
	}
	greet() { // overide the parent method
		return 'Hello ' + this.firstname;
	}
}

var wang = new InfomalPerson('WANG','Xi');
console.log(wang.greet());// Hello WANG
```
---

## Odds and Ends

### typeof , instanceof
```JavaScript
var a = 3;
console.log(typeof a); // number

var b = 'Hello';
console.log(typeof b); // string

var c = {};
console.log(typeof c); // object

var d = [];
console.log(typeof d); // object ,  is weird
console.log(Object.prototype.toString.call(d)); // [Object Array] , it's better

function Person(name) {
	this.name = name;
}

var e = new Person('William');
console.log(typeof e); // object , function is object in JavaScript
console.log(e instanceof Person); // true

console.log(typeof undefined);// undefined
console.log(typeof null); // object, a bug in JavaScript
```

### Strict Mode [Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)


```JavaScript
var person;
persom = {}; //mistapping on purpose
console.log(typeof persom);// object
```
We don't want this happen, because sometimes it makes code very difficult to debug, we want the complier to make sure that every time we use a variable, it has to be declared.  
We can use 'Strict Mode' to tell the complier to do this.
```JavaScript
"use strict"; // add this to the code

var person;
persom = {};  // Error 
console.log(typeof persom);
```



