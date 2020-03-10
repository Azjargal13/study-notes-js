# Javascript question #2

resources used:
- https://developer.mozilla.org/en-US/docs/Glossary/Hoisting

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
