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

 8. What is event delegation?
 - Event delegation is the idea that if you have a lot of elements handled in a similar way, instead of assigning a handler to each of them, you put a single handler on their common ancestor. In the handler, you get event.target, check if the target is something you want to act on, then handle it. This way, if you wanted to do the same thing for many similar elements, you can put the event listener on their common ancestor rather than on each element

## ES5 vs ES6 

9. Discuss 4 differences between ES5 and ES6 that you find important
- 1. ES6 allows block scoping, meaning a new scope will be defined for every set of curly braces. This prevents us from polluting the global scope and allows for easier function writing
2. 'let' and 'const' are used in ES6 instead of 'var' from ES5. These new keywords are not hoisted and prevent duplicate variable declaration
3. Lexical 'this' using arrow functions. When using arrow functions in ES6, you can force 'this' to point to th object it is physically located in (instead of the global scope)
4. Class structure allows JavaScript to be written more similarly to OO languages

## Error Handling

10. What are the steps of a try..catch block in Javascript?
- First, the code in the try block is executed. If there were no errors, the catch block is skipped. If an error occurs, the try execution is stopped and the catch block is run. It will execute actions for errors that it recognizes and rethrow all other errors. If a finally block is executed, it is always run, either after the try block is finished or the catch block is.

11. What type of errors to try..catch blocks work for?
- try..catch blocks only work for RuntimeErrors
