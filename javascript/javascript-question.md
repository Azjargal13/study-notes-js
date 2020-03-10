# Javascript question

**Q: How prototypal inheritance works?**

Resources used:
- https://medium.com/@kevincennis/prototypal-inheritance-781bccc97edb
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
- https://www.quora.com/Whats-a-typical-use-case-for-anonymous-functions-in-JavaScript?share=1
# Prototypal inheritance

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