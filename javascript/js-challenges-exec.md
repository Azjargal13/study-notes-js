# JS Challenge solve
In this section, will solve JS challenges of self-invoking functions, closures, conditionals, properties, loop, ghost array and so on.

- resource used:
  - https://tcorral.github.io/javascript-challenges-book/conditionals_functions/README.html
# Self invoking functions

```js
var testValue;
function test() { testValue = 3; }();

// testValue -> undefined
// test() is not executed,throws Syntax error,Unexpected token ')'

// to fix the error
!function test(){ testValue=3}()

// returns `true`
// testValue = 3 but test() is can not be called
// ReferenceError, test is not defined.

```

# Float operations Imprecision

```js
// js floating points

var stockOptionsCost = 10.70, paid = 20.80;
var stock =  (paid - stockOptionsCost).toFixed(2);

// return stockOptionsCost =  10.100000000000001
// return stock = 10.10

```

# Hoisting and Conditionals statement

```js
var bird = 'Pidgeons';
( function () {
    if ( typeof bird === 'undefined' ){
        var bird = 'Rubber Duck';
        console.log('Ernie loves his ' + bird );
    } else {
        console.log('Bert loves his ' + bird );
    }
}() );

// returns: Ernie loves his Rubber Duck
```

It is because `bird` variable is defined as global and in self invoking function it checks `bird` (global var) type, instead it reads `bird` (inside self-invoking func()) var. JS has no block var.

To fix this, we can set `bird` inside self-invoking func as local, declare with `let`. So we can see 
```js
var bird = 'Pidgeons';
( function () {
    if ( typeof bird === 'undefined' ){
        let bird = 'Rubber Duck';
        console.log('Ernie loves his ' + bird );
    } else {
        console.log('Bert loves his ' + bird );
    }
}() );

// Bert loves his Pidgeons
```

# Checking properties

```js
var key,
    obj = {
        name: 'john',
        surname: 'doe'
    };


for ( key in obj ) {
    if ( obj.hasOwnProperty( key ) ) {
       console.log( key + ' exists in obj' );
       console.log( key + ': ' + obj[key] );
       continue;
    }
    console.log( key + " doesn't exist in obj" );
}

// name exists in obj
// name: john
// surname exists in obj
// surname: doe

```

But we can result of 

```
name doesn't exist in obj
surname exists in obj
surname: doe
```

For that we can do this,

```js
var key,
    obj = {
        name: 'john',
        surname: 'doe'
    };

Object.prototype.hasOwnProperty = function (key) {
    if(key == 'name'){
        return false;
    }
    return true;
};

for ( key in obj ) {
    if ( obj.hasOwnProperty( key ) ) {
       console.log( key + ' exists in obj' );
       console.log( key + ': ' + obj[key] );
       continue;
    }
    console.log( key + " doesn't exist in obj" );
}
```

We can set object property by accessing `Object.prototype.hasOwnProperty`.

# Closures and Objects

JS has two ways of data receiving as a function argument.
- Primitives passed by copy
- Objects are passed by reference

```js
var oPerson = { name: 'john' };

(function(oTeacher) {
   window.getTeacher= function() {
      console.log(oTeacher);
   };
}(oPerson));

window.getTeacher();

oPerson.surname = 'doe';

window.getTeacher();

oPerson = { name: 'mary', surname: 'sullivan' };

window.getTeacher();
```

In this case, first `oPerson` var is declared as Object.
When first time `window.getTeacher()` get called, it returns `oPerson` (obj).

After some properties added in `oPerson`, it returns updated `oPerson` obj value.

When we again assign `oPerson` (completely new value) then calling `window.getTeacher()` it is returning already stored reference. Because the closure has stored the reference in the memory for oTeacher, being referenced inside the closure.

### NOTE: 
This is happening because when the closure has been executed it has saved the reference in memory for oPerson as oTeacher and even when oPerson has changed the assigned value to a different object it continues being referenced inside the closure. It is important to check this problems because if you make the same with DOM elements and the element is removed from the DOM tree you will get memory leaks issues.

To fix this issue, simply we should not use closure.

```js
var oPerson = { name: 'john'};

window.getTeacher= function() {
  console.log(oPerson);
};

window.getTeacher();

oPerson.surname = 'doe';

window.getTeacher();

oPerson = { name: 'mary', surname: 'sullivan' };

window.getTeacher();
```

# Conditionals and Functions

```js
// snippet1
var test;

if ( true ) {
    // func expression
    test = function () {
        console.log( "That's true" );
    };
} else {
    test = function () {
        console.log( "That's false" );
    };
}

test(); // Shows "That's true"
```

The execution of Snippet 1 shows "That's true" because function expressions are evaluated in execution time.
```js
//snippet2

if ( true ) {
    // func declaration
    function test() {
        console.log( "That's true" );
    }
} else {
    function test() {
        console.log( "That's false" );
    }
}

test(); // Shows "That's false"
```

The execution of Snippet 2 shows "That's false" because function declarations are evaluated in evaluation time, and the second one overwrittes the first one.

```js
// snippet3
var test;

if ( true ) {
    // func expression
    test = function () {
        console.log( "That's true" );
    };
} else {
    // func declaration
    function test() {
        console.log( "That's false" );
    }
}

test(); // Shows "That's true"
```

The execution of Snippet 3 shows "That's true" because when the code has been evaluated it has changed to the function that could return "That's false" but when the code has been executed it has been overwritten again with the function expression.

# Delete operator

Removes a property from an object; if no more references to the same property are held, it is eventually released automatically.

```js
const Employee = {
  firstname: 'John',
  lastname: 'Doe'
}

console.log(Employee.firstname);
// expected output: "John"

delete Employee.firstname;

console.log(Employee.firstname);
// expected output: undefined

```
the `delete` operator has nothing to do with directly freeing memory. Memory management is done indirectly via breaking references.

**Prototype chain**

```js
function Foo() {
  this.bar = 10;
}

Foo.prototype.bar = 42;

var foo = new Foo();

// foo.bar is associated with the 
// own property. 
console.log(foo.bar); // 10 

// Delete the own property within the 
// foo object. 
delete foo.bar; // returns true 

// foo.bar is still available in the 
// prototype chain. 
console.log(foo.bar); // 42 

// Delete the property on the prototype.
delete Foo.prototype.bar; // returns true 

// The "bar" property can no longer be 
// inherited from Foo since it has been 
// deleted. 
console.log(foo.bar); // undefined
```

# With single code detect IE

```js
function isIE() {
    window.external = '';
    return typeof window.external === 'object';
}
```

NOTE: As of 2020, `window.external` is deprecated. So advised not to use.

# Character encoding 

```js
console.log( '#2:', 'mañana' === 'mañana' );
// returns false
```

The reason its returning false is UTF8 encoding is encoded character n and ~, which is different from ñ character.

