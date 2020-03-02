
# JS Function

any var is belong to either local or global scope. Global var can be made local closures.

A func can enter all var inside func 

```js
function example(){
    let a = 1
    console.log('func access var inside of func',a)
}
```

Also func can get var (access) outside the func.
```js
var a = 1
function example(){
    console.log('func access var outse of func',a)
}
```

| Local var                                                                                                | Global var                                                                                                                               |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Local var can be used only inside the func. Hidden from other func or scripts                            | In a web page, global var belongs to the window obj. Any global var can be used or changed by all scripts in the page and in the window. |
| Local var lifetime is short. When func is invoked local var created. And del when func exec is finished. | Global var live until the page is closed or navigate other pages/window.                                                                 |


**NOTE**

any var created without `var, let, const` are always global, even if they created inside a func.

# JS Inner function

in JS, all func have access to the scope above them, means inner func always can be accessible to its outer func.

JS supports nested func.

```js
// lexical scoping
function counter(){
    var count=0
    function plus(){counter += 1}
    plus()
    return count
}
```
In this case, `plus()` can access var `count` and able to increment.  


## What is a closure?

```js
var count = (function (){
    var counter=0
    return function(){
        counter+=1
        return counter
    }
})
```
This is self-invoking func. var `count` is assigned the return value of a self-invoking func. 
Closure makes possible to have private var. `counter` is protected by the scope of anonymous func, can only be changed using add func.

Self invoking function runs only once. It can access the counter of the parent scope. 

Closure is a func that can get var to the parent scope, even after the parent func is closed.

Closure is created every time a func is created, at func creation time.