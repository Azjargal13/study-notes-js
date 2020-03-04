# Objects and classes

# `this` keyword

Automatically defined in the scope of every func.

`this` passing along the object reference. It's a **run time binding**. 

Contextual based on the conditions of the function's invokations. Where the function is called is really matter for `this`.

When function is invoked, activation record or otherwise known as execution context is created. This record contains info about where the func was called from (the callstack), how func is invoked, what parameters are passed. One of the property of the record is `this` ref will be used for the duration of the func's exec.

This is neither ref to a func itself, nor is it a ref to the function's lexical scope.

What is reference is determined by the call-site where function is called.