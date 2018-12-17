# Week 2

## Hoisting

1. In which phase does hoisting occur?
- Compilation

2. What is the difference between function hoisting and variable hoisting?
- Function decalarations are completely hoisted, meaning they can be called before they are defined. Variables are partially hoisted. Var declarations are hoisted, but not assignment (will show up as undefined if used before assignment). const and let are not hoisted (will throw reference error if used before assignment)

## 'new' keyword

3. What does the new keyword do in Javascript?
-   1. Creates a new object
    2. Sets the object's prototype to be the prototype of the constuctor function
    3. Executes the constructor function with 'this' as the newly created object
    4. Returns the created object. If the constructor returns an object, this object is returned.

4. What type of function is invoked with the new keyword? What does this function return?
- Functions invoked using the new keyword are called constuctor functions. It returns a new object with a prototype set to the prototype of the constuctor function and any properties defined on the contructor function.

 ## Event Bubbling

 5. How can you stop event bubbling?
 - By using event.stopPropagation(). This will stop the movement upwards, but all event handlers on the current element will still run. It is not advised to stop event bubbling unless you have a very good reason to, as you may need this behavior later for different reasons.

 6. What is the difference between event.target and event.currentTarget?
 - event.target is the most deeply nested argument that caused the event and doesn't change while event.currentTarget is the element that has the currently running handler on it. These could be the same element

 7. What does stopImmediatePropagation do?
 - It stops bubbling from going upwards and prevents handlers on the current element from executing

