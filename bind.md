The bind() method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.
#[Function.prototype.bind() from MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
##Creating a bound function
The simplest use of bind() is to make a function that, no matter how it is called, is called with a particular this value. A common mistake for new JavaScript programmers is to extract a method from an object, then to later call that function and expect it to use the original object as its this (e.g. by using that method in callback-based code). Without special care, however, the original object is usually lost. Creating a bound function from the function, using the original object, neatly solves this problem:
```js
this.x = 9; 
var module = {
  x: 81,
  getX: function() { return this.x; }
};

module.getX(); // 81

var retrieveX = module.getX;
retrieveX(); 
// 9, because in this case, "this" refers
// to the global object

// Create a new function with 'this' bound to module
// New programmers (like myself) might confuse the
// global var getX with module's property getX
var boundGetX = retrieveX.bind(module);
boundGetX(); // 81
```
##Partially applied functions (currying)
The next simplest use of bind() is to make a function with pre-specified initial arguments. These arguments (if any) follow the provided this value and are then inserted at the start of the arguments passed to the target function, followed by the arguments passed to the bound function, whenever the bound function is called.
```js
function list() {
  return Array.prototype.slice.call(arguments);
}

var list1 = list(1, 2, 3); // [1, 2, 3]

// Create a function with a preset leading argument
var leadingThirtysevenList = list.bind(undefined, 37);

var list2 = leadingThirtysevenList(); 
// [37]

var list3 = leadingThirtysevenList(1, 2, 3);
// [37, 1, 2, 3]
```
##With setTimeout
By default within window.setTimeout(), the this keyword will be set to the window (or global) object. When working with class methods that require this to refer to class instances, you may explicitly bind this to the callback function, in order to maintain the instance.
```js
function LateBloomer() {
  this.petalCount = Math.ceil(Math.random() * 12) + 1;
}

// Declare bloom after a delay of 1 second
LateBloomer.prototype.bloom = function() {
  window.setTimeout(this.declare.bind(this), 1000);
};

LateBloomer.prototype.declare = function() {
  console.log('I am a beautiful flower with ' +
    this.petalCount + ' petals!');
};

var flower = new LateBloomer();
flower.bloom();  
// after 1 second, triggers the 'declare' method
```
