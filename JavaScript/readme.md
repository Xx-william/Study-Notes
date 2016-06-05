#JavaScript Learning Notes
- - - - -
##Execution Contexts and Lexical Environments


- **this**
       In the inspector( in the navigator ) under the console window, we can type 'this'         to see all the global object. 

- **console.log()**
## Types and Operators
###Type
- **undefined** - key word
    the variable is created in the memery but has no value.

- **null**
- **boolean**
- **number**
- **String** is primitive type in JavaScript
- **symbol** used in ES6

###Operator ' == ' and ' === '
- **' a == b  '**  - Equality - If  a and b have the same value
- **' a === b '** - Strict Equality - If a and b have the same value and if a and b have the same type

###Existence and Boolean
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
##Objects and Functions
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
###Array
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







