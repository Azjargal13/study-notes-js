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

