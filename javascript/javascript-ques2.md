# Javascript question #2

resources used:
- https://developer.mozilla.org/en-US/docs/Glossary/Hoisting
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
- https://developers.google.com/web/updates/2015/01/ES6-Template-Strings
- https://developer.mozilla.org/en-US/docs/Glossary/IIFE
- https://stackoverflow.com/questions/1013385/what-is-the-difference-between-a-function-expression-vs-declaration-in-javascrip#3344397
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map

**Q:Explain "hoisting"**

# Hoisting

with a help of context execution works in JS, hoisting works well.
The var can be initialized and used before it is declared.

Example:
```js
catName("Chloe");

function catName(name) {
  console.log("My cat's name is " + name);
}
/*
The result of the code above is: "My cat's name is Chloe"
*/
```

Remember!, only declarations are hoisted not initializations.
```js
console.log(num); // Returns undefined, as only declaration was hoisted, no initialization has happened at this stage 
var num; // declaration
num = 6; // initialization
```
**Q:Give an example of generating a string with ES6 Template literals**

# Template literals

String literals allowing embedded expressions. (simple back-ticks `` not '' or "", to escape a backtick in a template literal, put a backslash (`\`) before the backtick)

- string expression 
- string text 
- multi-line string text
- string text ${expression}

```js
// expression interpolation
var name="Aza"

console.log(`Hey, how r u doing ${name}?`)
// Hey, how r u doing Aza?

// multi-line string text
console.log(`first line
second line
third line`)
// first line
// second line
// third line
```

**Q: Difference between `while` and `do-while` loops in JS?**

# `while` |  `do-while`

The `while` statement creates a loop that executes a specified statement as long as the test condition evaluates to true. The condition is evaluated before executing the statement.

```js
let n = 0;

while (n < 3) {
  n++;
}

console.log(n);
// expected output: 3

```
Note: Use the break statement to stop a loop before condition evaluates to true.

The do...while statement creates a loop that executes a specified statement until the test condition evaluates to false. The condition is evaluated after executing the statement, resulting in the specified statement executing at least once.

```js
let result = "";
let i = 0;

do {
  i = i + 1;
  result = result + i;
} while (i < 5);

console.log(result);
// expected result: "12345"

```

Difference is their execution. `while` evaluates before exec, whereas `do-while` executes after exec, which means at least specified statement will be executed once surely.

**Q: What are the benefits of using spread syntax and how is it different from rest syntax?**

# spread syntax `...`

Allows iterable such as array expression, string, object expression to be expanded.

```js
function sum(x, y, z) {
  return x + y + z;
}

const numbers = [1, 2, 3];

console.log(sum(...numbers));
// expected output: 6

console.log(sum.apply(null, numbers));
// expected output: 6

```

Spread in function calls, replace `apply()`.
Its common to use `apply()` in cases where elements of an array as an args to a func.

```js
function myFunction(x, y, z) { }
const args = [0, 1, 2];
myFunction.apply(null, args);
```

with `...` we can replace same as below
```js
function myFunction(x, y, z) { }
const args = [0, 1, 2];
myFunction(...args);
```

Array literal

can use `...` instead of `push()`, `concat()`, `slice()`
```js
const parts = ['shoulders', 'knees']; 
const lyrics = ['head', ...parts, 'and', 'toes']; 
```

Copy array

```js
const arr = [1, 2, 3];
const arr2 = [...arr]; // like arr.slice()

arr2.push(4);
```

Concat array

```js
const arr1 = [0, 1, 2];
const arr2 = [3, 4, 5];

arr1 = [...arr1, ...arr2]; 
//  arr1 is now [0, 1, 2, 3, 4, 5]

// replace using concat
arr1 = arr1.concat(arr2);

// replace `unshift()`
arr1 = [...arr2, ...arr1]; 
//  arr1 is now [3, 4, 5, 0, 1, 2]
```

# Rest syntax

Rest syntax looks exactly like spread syntax, but is used for destructuring arrays and objects.

In a way, rest syntax is the opposite of spread syntax. Spread syntax "expands" an array into its elements, while rest syntax collects multiple elements and "condenses" them into a single element. 

The rest parameter syntax allows us to represent an indefinite number of arguments as an array.

A function's last parameter can be prefixed with ... which will cause all remaining (user supplied) arguments to be placed within a "standard" Javascript array.

Only the last parameter can be a "rest parameter".

```js
function myFun(a, b, ...manyMoreArgs) {
  console.log("a", a)
  console.log("b", b)
  console.log("manyMoreArgs", manyMoreArgs)
}
myFun("one", "two", "three", "four", "five", "six")

// Console Output:
// a, one
// b, two
// manyMoreArgs, [three, four, five, six]
```

Destructing rest parameters
```js
function f(...[a, b, c]) {
  return a + b + c;
}

f(1)          // NaN (b and c are undefined)
f(1, 2, 3)    // 6
f(1, 2, 3, 4) // 6 (the fourth parameter is not destructured)
```

**Q:Why you might want to create static class members?**

# static class member

Static class members usually used as utility functions. Static methods aren't called on instances of the class. These method calls are made directly on the class.

```js
class ClassWithStaticMethod {
  static staticMethod() {
    return 'static method has been called.';
  }
}

console.log(ClassWithStaticMethod.staticMethod());
// 'static method has been called.'

// if we call the method on instance

c = new ClassWithStaticMethod()
c.staticMethod()

// TypeError: c.staticMethod is not a function
```

Static method can be accessed with constructor.

```js
class StaticMethodCall {
  constructor() {
    console.log(StaticMethodCall.staticMethod()); 
    // 'static method has been called.' 

    console.log(this.constructor.staticMethod()); 
    // 'static method has been called.' 
  }

  static staticMethod() {
    return 'static method has been called.';
  }
}

StaticMethodCall.staticMethod()
// static method has been called.

c = new StaticMethodCall()
c.constructor.staticMethod()

// static method has been called.
```

**Q: Expression and declarion difference**

# Expression vs Declaration

Calling them is exactly same. Difference is how the browser loads them into execution context.

Function declarations are load before any code is executed.

Function expressions load when the interpreter reaches that line of code.

If trying to call function expression before it's loaded, error will be thrown. No code can be called until all declarations are loaded.

```js
// function declaration

// as explained earlier, declarations always load before code exec
// can be called as

alert(foo())
// alert will be shown

function foo(){
  return 'something'
}

```

```js
// function expression

// named function expression

var foo = function bar(){
  return 'something'
}

// anonymous function expression

var foo = function(){
  return 'something'
}
```

`foo()` can be called after its creation.

# Immediately-invoked function expression (IIFE)
runs as soon as it is defined.
Also known as self-executing anonymous function.

contain two major parts:

 - enclosed with grouping operator ()
 - function expression ()

Function becomes a function expression which is immediately executed. The var within the expr can not be accessed from outside it.

```js
// IIFE
(function(){
  var foo = "bar"
})()

foo 

// will throw error
```
Assigning the IIFE to a variable stores the function's return value, not the function definition itself.

```js
var result = (function () {
    var name = "Aza"; 
    return name; 
})(); 
// Immediately creates the output: 
result; // "Aza"

```

**Q: Why is it called a Ternary operator, what does the word "Ternary" indicate?**

# Ternary operator

JS operator that takes three operands, condition followed by a  `?` then expression to execute if the condition is truthy `:` then finally the expression to execute if the condition is falsy.

Shortcut of `if` statement.

```js

function getFee(isMember) {
  return (isMember ? '$2.00' : '$10.00');
}

console.log(getFee(true));
// expected output: "$2.00"

console.log(getFee(false));
// expected output: "$10.00"

console.log(getFee(1));
// expected output: "$2.00"

```

Conditional chains

```js
function example(…) {
    return condition1 ? value1
         : condition2 ? value2
         : condition3 ? value3
         : value4;
}

// Equivalent to:

function example(…) {
    if (condition1) { return value1; }
    else if (condition2) { return value2; }
    else if (condition3) { return value3; }
    else { return value4; }
}
```


**Q: What is strict mode? What are some of the advantages/disadvantages of using it?**

# `use-strict`

Strict mode, introduced in EC5.

Changes to normal JS semantics
- eliminate some JS silent errors by changing them to throw errors
- fixes mistakes that make it difficult for JS engines to perform optimizations: strict mode sometimes can run faster
- prohibits some syntax likely to be defined in future versions of ESnext

Strict mode changes syntax and runtime behavior.
Changes making easier to write secure JS.

**Q:Difference between `Array.forEach()` and `Array.map()`?**

# Array.forEach()

The forEach() method executes a provided function once for each array element.
There is no way to stop or break a forEach() loop other than by throwing an exception. If you need such behavior, the forEach() method is the wrong tool.

Early termination may be accomplished with:

 - A simple for loop
 - A for...of / for...in loops
 - Array.prototype.every()
- Array.prototype.some()
 - Array.prototype.find()
 - Array.prototype.findIndex()

Array methods: every(), some(), find(), and findIndex() test the array elements with a predicate returning a truthy value to determine if further iteration is required.

# Array.map()

The map() method creates a new array populated with the results of calling a provided function on every element in the calling array.

Since map builds a new array, using it when you aren't using the returned array is an anti-pattern; use forEach or for-of instead.

You shouldn't be using map if:

 - you're not using the array it returns; and/or
 - you're not returning a value from the callback.

**Q: Difference between method and function in JS?**

# Method
In JavaScript every function is an object. An object is a collection of key:value pairs. If a value is a primitive (number, string, boolean), or another object, the value is considered a property. If a value is a function, it is called a `method`.

Method : Method is a function when object is associated with it.

```js
var obj = {
name : "John snow",
work : function someFun(paramA, paramB) {
    // some code..
}
```
# Function

Function : When no object is associated with it , it comes to function.

```js
function fun(param1, param2){
// some code...
}
```