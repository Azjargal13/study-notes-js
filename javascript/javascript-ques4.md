# Javascript coding question #1

### Q1: What is the value `a` return?
```js
var a = 10 + "20"

// return: "1020"
```

In JavaScript, numbers joined to a string result in a string, not a number.
It does this because JavaScript executes from left to right by default.

We solve the problem by wrapping the parts we want to be added together first in parentheses:

### Q2: What is the value `a` return?

```js
var a = 0.1 + 0.2
a == 0.3

// return `false`

var x = (0.2 * 10 + 0.1 * 10) / 10;       // x will be 0.3
```
JavaScript numbers are always 64-bit floating Point. Unlike many other programming languages, JavaScript does not define different types of numbers, like integers, short, long, floating-point etc.

JavaScript numbers are always stored as double precision floating point numbers, following the international IEEE 754 standard.

### Q3: JS Numeric string
```js
var x = "100";
var y = "10";
var z = x / y;       // z will be 10

var x = "100";
var y = "10";
var z = x * y;       // z will be 1000
```

JavaScript will try to convert strings to numbers in all numeric operations.
```js
var x = 0xFF;        // x will be 255
```
JavaScript interprets numeric constants as hexadecimal if they are preceded by 0x.