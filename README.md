# ClassesES6

# Welcome to our lesson on classes with ES6!

## Learning Objectives
 - Be able to create a class constructor in ES6
 - Use extends to inherit class properties
 - Define what "super" does within ES6 classes
 
 ## Intro
 We have briefly used classes and prototypes in Javascript to do Object Oriented Program - we all are familiar with the shtick of defining objects with key value pairs and we are perhaps a little less
 familiar with defining prototypes that pass through objects in inheritance.
 
 Here's an example of classes in ES5: 
 
 ```
 function Sandwich(type) {
  this.type  = type;
  this.bread = "multigrain;
  this.snarf = snarf;
  }
  
  function snarf() {
  console.log("I'm snarfing on a " + this.type + " on" + this.bread + "sandwich");
  }
  ```
  In other languages (like PHP and Java) inheritance is something baked into classes. In Javascript (ES5 style) you can create inheritance and we seen using prototypes (there are other ways as well). So something like: 
  
  ```
  function BLT() {
  this.bacon = true;
  }
  BLT.prototype = new Sandwich("Layered");
  ```
  
  ## ES6 Version
  
  ES6 allows you to create inheritance in a much simpler manner. Behold! 
  
  ```
  class Kingdom {
  constructor(name, area) {
  	this.name = name;
  	this.area = area;
}

	declare() {
      console.log("I belong to the Kingdom of ", this.name + '.');
 
    }
}

class Knight extends Kingdom{
  constructor(weapon, name, area){
    super(name, area);
    this.weapon = weapon;
  }
  fight() {
    super.declare()
    console.log("I wield a " + this.weapon);
    
  }
}

var jon = new Knight("sword", "England", "England");
jon.fight();
  ```
  
  In the above example, you can see a few interesting things:
   - constructor allows us to pass in properties to our object!
   - extends allows us to pass along inherited properties!
   - super allows us to access properties in the parent object!
 
One slight catch - make sure to declare super before you refer to "this" in your child object - otherwise you will get a reference error!

## Comparison
 Lets look at what we do know: 
 IN ES6
 
 ```
 class Polygon //define a class
{ 
	constructor(height, width) //class constructor
	{
	this.name   = "Polygon"; //constructor properties
  	this.height = height; //defines the height of this class as the variable hight thats passed in
  	this.width  = width;
  	}
  	
  	sayname() //define main constructor function
  	{
  	console.log("Hi, I am a "   + this.name   + ".");
    	console.log("My height is " + this.height + ".");
    	console.log("My width is "  + this.width  + ".");
  	}
}

class Rectangle extends Polygon //inheretence
{
	constructor(height, width)
  	{
  	super(height, width); //calls parent constructor
  	this.name = "Rectangle";//we passed in length as the parent constructor height
  	}
  get area()
  {
  	return (this.height * this.width); 
  }
}
let s = new Rectangle(5, 5);

s.sayname();
console.log(s.area);
```

this concept seems pretty simple and frankly should have been available in ES5 right? 
Well, how would we do this in ES5? 

Well... first we would need to "use strict"
```"use strict";```
remember, now we are entering a different set of JavaScript rules so we can restrict the amount of global variables defined even though thats probably much easier in this contrived example. Why would we want to do that? 
See, the whole point of inheretence of classes is that we can attach new instances of that class to properties defined for the constructor. So even though it may be easier to define global variables and act on individual functions of that instance, it doesnt accomplish the goal of inheretence. That being said:

we would then need to define functions to be called to mimick the relationship that inheretence provides: 
```
var _createClass = function () 
{ //creating the class definition function
	function defineProperties(target, props) 
	{  //creating the property definitions...definition for that function
		for (var i = 0; i < props.length; i++) 
		{ 
			var descriptor = props[i]; 
			descriptor.enumerable = descriptor.enumerable || false; 
			descriptor.configurable = true; 
			if ("value" in descriptor) 
				descriptor.writable = true; 
				Object.defineProperty(target, descriptor.key, descriptor); 
		} 
	} 
	return function (Constructor, protoProps, staticProps) 
	{ 
	if (protoProps) defineProperties(Constructor.prototype, protoProps); 
	if (staticProps) defineProperties(Constructor, staticProps); return Constructor; 
	}; 
}();
```
Here we are defining the object of properties... as a part of the object of the class... that we defined. Right? 
## Then

we would have to define the possible returns of a constructor
```
function _possibleConstructorReturn(self, call) 
{ 
	if (!self) //error handling that is evident in ES6
	{ 
		throw new ReferenceError("this hasn't been initialised - super() hasn't been called"); 
	} 
	return call && (typeof call === "object" || typeof call === "function") ? call : self; 
} 
//So whether the constructor is an object or a method, we are just returning that constructor as long as the inheretence of a subclass has been declared in relation to the class defined before it.
```
But how do we know that a subclass is in relation to a superclass...what inherets what? at this point the only thing we can do is create classes and return constructors.
well.....THATS ANOTHER FUNCTION 
```
function _inherits(subClass, superClass) 
{ 
	if (typeof superClass !== "function" && superClass !== null) 
		{ 
			throw new TypeError("Super expression must either be null or a function, not " + typeof superClass); 
		} 
	subClass.prototype = Object.create(superClass && superClass.prototype, 
		{ 
			constructor: { value: subClass, enumerable: false, writable: true, configurable: true } 
		}); 
	if (superClass) Object.setPrototypeOf ? Object.setPrototypeOf(subClass, superClass) : subClass.__proto__ = superClass; 
}
```
Whats also cool about this is that ES6 will check to make sure that the class you've defined is not a function and that it is simply an object with a constructor function and a main function. 
```
function _classCallCheck(instance, Constructor) 
{ 
	if (!(instance instanceof Constructor)) 
	{ 
		throw new TypeError("Cannot call a class as a function"); 
	} 
}
```
Now that we have defined the relationships between sub and super classes, we can instantiate classes that relate to the parent class definition by calling these methods... it should look something like this. 

```
var Polygon = function () 
{ //define a class
  function Polygon(height, width) //class constructor
  {
    _classCallCheck(this, Polygon);

    this.name   = "Polygon"; //constructor properties
    this.height = height;
    this.width  = width;
  }

  _createClass(Polygon, 
  [{
    key: "sayname",
    value: function sayname() //define main constructor function
    {
      console.log("Hi, I am a " + this.name + ".");
      //console.log("My height is " + this.height + ".");
      //console.log("My width is "  + this.width  + ".");
    }
  }]);

  return Polygon;
}();

var Rectangle = function (_Polygon) 
{
  _inherits(Rectangle, _Polygon);

  function Rectangle(height, width) 
  {
    _classCallCheck(this, Rectangle);

    //calls parent constructor
    var _this = _possibleConstructorReturn(this, (Rectangle.__proto__ || Object.getPrototypeOf(Rectangle)).call(this, height, width));

    _this.name = "Rectangle"; //we passed in length as the parent constructor height
    return _this;
  }

  _createClass(Rectangle, 
  [{
    key: "area",
    get: function get() 
    {
      return this.height * this.width;
    }
  }]);

  return Rectangle;
}(Polygon);

var s = new Rectangle(5, 5);

s.sayname();
console.log(s.area);
```

#Spread
<p align="center">
    <img src="http://media1.giphy.com/media/Jfu3UlHpJK1Hi/giphy.gif">
</p>

###Syntax
For function calls:
```javascript
myFunction(...iterableObj);
```

For arrays:
```javascript
[4, 3, ...iterableObj, 6]
```

###What does it do?
[From MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator):


>In ES6, spread syntax allows an expression to be expanded in places where multiple arguments (for function calls) or multiple elements (for array literals).

Simply put, the spread syntax can be used to access all of the elements of an iterable data structure.

```javascript
var foo = [4, 6];

var bar = [1, ...foo, 2, 5];     // [1, 4, 6, 2, 5]
```
or
```javascript
function myFunction(a, b, c) {
  return a + b + c;
}

var foo = [1, 2, 4];

myFunction(...foo)   // 6
```

### Why use it?
List concatenation is now simple and inuitive:
```javascript
var jamesList = ['james', 'jim', 'jimbo', 'jimothy'];
var andyList = ['andy', 'andrew', 'drew', 'a-dog'];
var nayanaList = ['nayana'];

var instructors = [...jamesList, ...andyList, ...nayanaList]
```

A good use case is a function that can take any number of arguments, e.g., `Math.max()`

```javascript
var arr = [1, 3, 15, 8, 9, 6];

Math.max(1, 3, 15, 8, 9, 6);    // 15

Math.max(arr);                  // NaN

Math.max(...arr);               // 15

```
