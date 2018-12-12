# Week 2

## Hoisting

* **Hoisting** the behavior of 'moving' var and function declarations to the top of their respective scopes during the compilation phase.

* Function declarations are completely hoisted. This means that a declared function can be called before it is defined

* Variables are partially hoisted. var decalarations are hoisted but not its assignments. let and const are not hoisted

## new keyword 

* The 'new' keyword invokes a function in a special way. Functions invoked using the new keyword are called constructor functions

* What does the new keyword actually do?
    1. Creates a new object
    2. Sets the object's prototype to be the prototype of the constuctor function
    3. Executes the constructor function with 'this' as the newly created object
    4. Returns the created object. If the constructor returns an object, this object is returned.