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

### Q4: Self execution function execution
```js
var foo = "Hello";
(function() {
  var bar = " World";
  alert(foo + bar);
})();
alert(foo + bar);

// execute self exec function 
// alert text will be "Hello World"
```

### Q5: Obj reference
```js

var foo = {n: 1};
var bar = foo;
foo.x = foo = {n: 2};

// foo value {n:1}
// foo gets new property x value of {n:2}
// bar value reference of foo

// bar = {n:1, x:{n:2}}
```

### Q6: Ordered execution
```js
console.log('one');
setTimeout(function() {
  console.log('two');
}, 0);
Promise.resolve().then(function() {
  console.log('three');
})
console.log('four');

// one
// four
// three
// wait for 0 ms
// two
```

### Q7: Return {}
```js

function foo1()
{
  return {
      bar: "hello"
  };
}

function foo2()
{
  return
  {
      bar: "hello"
  };
}

// foo1()
// {bar:"hello"}
// foo1().bar
// "hello"


// foo2()
// undefined

// reason is due to bracket return {}
```
