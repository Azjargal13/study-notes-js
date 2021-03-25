# Effective JS book notes

# Chapter 1: Accustoming yourself to JS

JS is used many areas such as 
- client side web programming
- server-side programs
- browser extension
- scripting for mobile
- scripting for desktop app

ES5 introduced `strict` mode, which can be applied by adding `use strict` in the code.

DO: 
Select any of `strict` mode or `non strict` mode policy for entire project.

**Things to remember #1:**
- Decide which version of JS will be used in project
- Be sure that any of your JS files can be run in any env
- Always test strict code in env that perform strict-mode check
- Beware of concat two different mode file (strict and non strict file)

**Things to remember #2:**
- JS numbers are `double precision` floating-point number
- Integers in JS are subset of doubles rather than a separate datatype
- Bitwise operator treat number as if they were 32 bit signed integer
- Be aware of limitation of precisions in floating-point arithmetic

**Things to remember #3:**
- Be aware of type coercion
  ```js
    3 + true // 4
    3 + false // 3
    "2" + 3  //"23"
    (1 + 2) + "3"; // "33"
    1 + "2" + 3; // "123"
    (1 + "2") + 3; // "123"
    "17" * 3; // 51
    "8" | "1"; // 9
  ```
   Since NaN is the only JavaScript value that is treated as unequal to itself, you can always test if a value is NaN by checking it for equality to itself:
  
  ```js
    var a = NaN;
    a !== a; // true
    var b = "foo";
    b !== b; // false
  ```
  Objects can also be coerced to primitives. This is most commonly used for converting to strings:  Objects are converted to strings by implicitly calling their toString method
    ```js
    Math.toString(); // "[object Math]"
    JSON.toString(); // "[object JSON]"
    ```
- Use typeof or comparison to undefined rather than truthiness to test for undefined values.
- Objects are coerced to numbers via `valueOf` and to strings via `toString`.
- Coercion rule

     ![Img]("https://github.com/Azjargal13/study-notes-js/blob/master/javascript/imgs/coersion-rule.PNG")
- Use `===` to make it clear to your readers that
your comparison does not involve any implicit coercions.
- Semicolons are only ever inserted before a } token, after one or more
newlines, or at the end of the program input.
Semicolons are only ever inserted when the next input token cannot be
parsed.

```js
return { };
// returns a new object, whereas the code snippet
```
```js
return
{ };
//parses as three separate statements, equivalent to:
return;
{ }
;
```
In other words, the newline following the return keyword forces an
automatic semicolon insertion, which parses as a return with no
argument followed by an empty block and an empty statement

# Chapter 2
**Things to remember #4**

- Avoid global var, keep use local var using `var` or `let` keyword
- JS facts about closure:
  - JS allows to refer to var that were defined outside of the current func.
  ```js
  function makeSandwich() {
  var magicIngredient = "peanut butter";
    function make(filling) {
    return magicIngredient + " and " + filling;
    }
  return make("jelly");
  }
  makeSandwich(); // "peanut butter and jelly"
  ```
  - Function can refer to var defined in outer functions even after those outer func have returned.

  ```js
    function sandwichMaker() {
      var magicIngredient = "peanut butter";
      function make(filling) {
      return magicIngredient + " and " + filling;
      }
      return make;
      }
    var f = sandwichMaker();
    f("jelly"); // "peanut butter and jelly"
  ```
  **Functions that
keep track of variables from their containing scopes are known as
closures.** The make function is a closure whose code refers to two outer
variables: magicIngredient and filling.
  - The third and final fact to learn about closures is that they can
update the values of outer variables. Closures actually store references
to their outer variables, rather than copying their values.
  ```js
  function box() {
  var val = undefined;
  return {
    set: function(newVal) { val = newVal; },
    get: function() { return val; },
    type: function() { return typeof val; }
  };
  }
  var b = box();
  b.type(); // "undefined"
  b.set(98.6);
  b.get(); // 98.6
  b.type(); // "number"
  ```
# Chapter 3: Working with Functions

## Function, Method and Constructor calls

```js
// function call

function hello(username) {
    return "hello, " + username;
}
hello("Aza"); // "hello, Aza"
```
This does exactly what it looks like: It calls the hello function and
binds the name parameter to its given argument.

Methods in JS, obj properties that are function.

```js
var obj = {
  name: function(){
    return "hello, " + this.username;
  }
  username: "Aza"
}
obj.name()

// "hello, Aza"
```
Call expression determines the binding of  `this` in method (call's receiver).
Method calls provide the object in which the method property is
looked up as their receiver.

Constructors in JS,
```js
function User(name, passwordHash) {
  this.name = name;
  this.passwordHash = passwordHash;
}
//Invoking User with the new operator treats it as a constructor:
var u = new User("aza",
"0ef33ae791068ec64b502d6cb0191387");
u.name; // "aza"
```
Unlike function calls and method calls, a constructor call passes a
brand-new object as the value of this, and implicitly returns the new
object as its result. The constructor function’s primary role is to initialize
the object.

## High order functions

Higher-order functions are nothing more than functions that take
other functions as arguments or return functions as their result.
Taking function as an arg often referred as callbacks,

```js
// HOF
function compareNumbers(x, y) {
  if (x < y) {
  return -1;
  }
  if (x > y) {
  return 1;
  }
return 0;
}
[3, 1, 4, 1, 5, 9].sort(compareNumbers); // [1, 1, 3, 4, 5, 9]
```

We can simplify above example using anonymous function
```js
[3, 1, 4, 1, 5, 9].sort(function(x, y) {
    if (x < y) {
    return -1;
    }
    if (x > y) {
    return 1;
    }
    return 0;
}); // [1, 1, 3, 4, 5, 9]
```
Learning to use higher-order functions can often simplify your code
and eliminate tedious boilerplate.

```js
var names = ["Fred", "Wilma", "Pebbles"];
var upper = names.map(function(name) {
  return name.toUpperCase();
});
upper; // ["FRED", "WILMA", "PEBBLES"]
```
Utility high-order function implementation
```js
function buildString(n, callback) {
  var result = "";
  for (var i = 0; i < n; i++) {
    result += callback(i);
  }
return result;
}

var alphabet = buildString(26, function(i) {
  return String.fromCharCode(aIndex + i);
});
alphabet; // "abcdefghijklmnopqrstuvwxyz"

var digits = buildString(10, function(i) { return i; });
digits; // "0123456789"

var random = buildString(8, function() {
  return String.fromCharCode(Math.floor(Math.random() * 26)
  + aIndex);
});
random; // "ltvisfjr" (different result each time)
```
**Things to remember:**

# Objects

Objects inherit from other objects. Every object is associated with some other object, known as its prototype.

- C.prototype is used to establish the prototype obj created by new C().
- Object.getPrototypeOf(obj) is the standard ES5 mechanism for retrieving obj's prototype obj.
- obj.__proto__ is a nonstandard way of retrieving obj's prototype obj.

```js
  function User(name, passwordHash) {
    this.name = name;
    this.passwordHash = passwordHash;
  }
  User.prototype.toString = function() {
  return "[User " + this.name + "]";
  };
  User.prototype.checkPassword = function(password) {
  return hash(password) === this.passwordHash;
  };
  var u = new User("sfalken",
  "0ef33ae791068ec64b502d6cb0191387");
```

User func comes with default prototype property.

When we create an instance of User with the new operator,
the resultant object u gets the object stored at User.prototype
automatically assigned as its prototype object.

Property lookups start by searching the object’s own properties;
for example, u.name and u.passwordHash return the current values
of immediate properties of u. Properties not found directly on u are
looked up in u’s prototype. Accessing u.checkPassword, for example,
retrieves a method stored in User.prototype.

User as **a class**, even though it consists of little
more than a function. `Classes in JavaScript are essentially the combination
of a constructor function (User) and a prototype object used
to share methods between instances of the class (User.prototype)`.

The User function provides a public constructor for the class,
and User.prototype is an internal implementation of the methods
shared between instances. Ordinary uses of `User` and `u` have no need
to access the prototype object directly.

**if someone calls this new version of User with new?**
Thanks to the **constructor override pattern**, it behaves just like it
does with a function call. This works because JavaScript allows the
result of a new expression to be overridden by an explicit return from
a constructor function. When User returns self, the result of the new
expression becomes self, which may be a different object from the one
bound to this.

**Things to remember**
- A class is a design pattern consisting of a constructor function and
an associated prototype.
- C.prototype determines the prototype of objects created by new C().
- Prefer the standards-compliant Object.getPrototypeOf to the nonstandard
__proto__ property.
- Never modify an object’s __proto__ property.
- Use `Object.create` to provide a custom prototype for new objects.
- check that the receiver value is a proper instance of User
  ``` js
  function User(name, passwordHash) {
  if (!(this instanceof User)) {
    return new User(name, passwordHash);
  }
  this.name = name;
  this.passwordHash = passwordHash;
  }
  ``` 
  This way, the result of calling User is an object that inherits from. User.prototype, regardless of whether it’s called as a function or as a
  constructor.
  ```js
  var x = User("baravelli", "d8b74df393528d51cd19980ae0aa028e");
  var y = new User("baravelli",
  "d8b74df393528d51cd19980ae0aa028e");
  x instanceof User; // true
  y instanceof User; // true
  ```
- Make a constructor agnostic to its caller’s syntax by reinvoking
itself with new or with Object.create.
-  Document clearly when a function expects to be called with new.
-  Prefer storing methods on prototypes over storing them on instance
objects.

## Closures

Use it for information hiding. Closures are an austere data structure.
`They store data in their enclosed variables without providing direct access to those variables.`
The only way to gain access to the internals of a closure is for the
function to provide access to it explicitly. In other words, `objects and
closures have opposite policies: The properties of an object are automatically
exposed, whereas the variables in a closure are automatically
hidden.`

```js
function User(name, passwordHash) {
    this.toString = function() {
      return "[User " + name + "]";
};
    this.checkPassword = function(password) {
      return hash(password) === passwordHash;
};
}
```
Notice how, unlike in other implementations, the toString and
checkPassword methods refer to name and passwordHash as variables,
rather than as properties of `this`.

**Things to remember**
- Closure variables are private, accessible only to local references.
- Use local variables as private data to enforce information hiding
within methods.