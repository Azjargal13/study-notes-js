# Object

object comes in two forms.
 - declarative (literal) form
 - constructed form

Declaritive or literal form, syntax looks like:
```js
var obj = {
    name:'name',
    value:'value'
}
```

Constructed form, syntax looks like:
```js
var obj = new Object()
obj.name = 'name'
```

What is difference between them?

The only diff is can add more key/value pairs in literal form, whereas constructed form object's properties needed to be added one by one.

## 6 primary types

language types in the specification:
(simple primitives except `object`)
- string
- number
- boolean
- null
- undefined
- object

`function` is sub-type of object, technically referred as a callable object.

## Contents of obj

Contents of an obj consist of values stored at specifically named locations, which we call `properties`.

In obj container stores properties names where properties act as a pointer (reference), to where the values are stored.

