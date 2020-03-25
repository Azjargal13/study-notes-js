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
     ![Img]("../imgs/coersion-rule.PNG")


