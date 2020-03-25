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

