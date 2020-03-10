# Javascript question #1

Resources used:
- https://medium.com/@kevincennis/prototypal-inheritance-781bccc97edb
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
- https://www.quora.com/Whats-a-typical-use-case-for-anonymous-functions-in-JavaScript?share=1
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply
# Prototypal inheritance

**Q: How prototypal inheritance works?**

remember: 'Objects inherit from Objects'.

When any function is created newly, it is automatically have a property called `protoype` which initialized as an empty object. (Because JS provides inheritance).

Inherited members are defined in prototype. It is a property containing an obj which you define members that you want to be inherited.

**Good to remember**

Constructors - any time see `new` keyword, following function is used as a constructor.

### Differential inheritance

JS uses an inheritance model called `differential inheritance`. It means method are not copied from parent to child. Instead, children have an 'invisible link' back to their parent obj.

JS engine looks for property name from object. If the obj does not have the property, it goes up 'property chain' to object's parent to search property. Internally it calls with `this` to child obj.

Example

```js
function Car(){

}

Car.prototype.drive = function(){
    console.log('unnnn')
}

var bmw = Car()
bmw.drive() // 'unnnn'

```

In this example, even though var `bmw` does not have method to `drive()` but it can access through prototype inheritance.

To set `prototype chain` we use `Object.create()` to create an empty obj that inherits from another object. Which means, prototype and methods can be accessible from inherited obj.

**Q: What's a typical use case for anonymous functions?**

# Anonymous function
 
No identifier (named) functions.


Use cases:
- pass them as argument to other func 
- to create closures
- Array.prototype.map usage
- Callbacks
- Execute inline codes 
- In promises

**Q:Can you explain what Function.call and Function.apply do? What's the notable difference between the two?**

resources used:

# call()

`call()` calls a function with given `this` value and arguments provided individually.
```js
func.call([thisArg[, arg1, arg2, ...argN]])
// thisArg | Optional : the value to use  `this` when calling func
// arg1, arg2, argN | Optional: arguments for the function
```

Example using `call()`
```js
function Product(name, price) {
  this.name = name;
  this.price = price;
}

function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}

function Toy(name, price) {
  Product.call(this, name, price);
  this.category = 'toy';
}

const cheese = new Food('feta', 5);
const fun = new Toy('robot', 40);
```
# apply()
Fundamentail difference between `apply()`, and `call()` is `call()` accepts an **argument list**, while `apply()` accepts a **single array of arguments**.

Example using `apply()`
```js
const array = ['a', 'b'];
const elements = [0, 1, 2];
array.push.apply(array, elements);
console.info(array); // ["a", "b", 0, 1, 2]
```

**Q: Explain `Function.prototype.bind`**

# bind()
It creates a new bound function (that wraps the original function obj) that when called, has its `this` keyword set to the provided value, with a given sequence of arg preceding any provided when the new func is called.

```js
func.bind(thisArg[, arg1[, arg2[, ...argN]]])
```

Example using `bind()`

```js
this.x = 9;    // 'this' refers to global 'window' object here in a browser
const module = {
  x: 81,
  getX: function() { return this.x; }
};

module.getX(); 
//  returns 81

const retrieveX = module.getX;
retrieveX();
//  returns 9; the function gets invoked at the global scope

//  Create a new function with 'this' bound to module
//  New programmers might confuse the
//  global variable 'x' with module's property 'x'
const boundGetX = retrieveX.bind(module);
boundGetX(); 
//  returns 81
```

