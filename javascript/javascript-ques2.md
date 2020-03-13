# Javascript question #2

resources used:
- https://developer.mozilla.org/en-US/docs/Glossary/Hoisting
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
- https://developers.google.com/web/updates/2015/01/ES6-Template-Strings

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

