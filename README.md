# ClassesES6

# Welcome to our lesson on classes with ES6!

## Learning Objectives
 - Be able to create a class constructor in ES6
 - Use extends to inherit class properties
 - Define what "super" does within ES6 classes
 
 ## Intro
 We have briefly used classes and prototypes in Javascript to do Object Oriented Program - we all are familiar with the shtick of defining objects with key value pairs and we are perhaps a little less
 familiar with defining prototypes that pass through objects in inheritance.
 
 Here's an example of inheritance and classes in ES5: 
 
 ```
 function Sandwich(type) {
  this.type = type;
  this.bread = "multigrain;
  this.snarf = snarf;
  
