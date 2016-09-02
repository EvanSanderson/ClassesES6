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
  this.type = type;
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

# A Final Cool Thing

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

class Sword extends Knight {
  constructor(name){
    super(name);
      this.length = "5 feet";
  }
}
var jon = new Knight("sword", "England", "England");
jon.fight();
var excalibur = new Sword("sword");
jon.sword = excalibur;
console.log(jon.sword); // What do you think this logs?

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