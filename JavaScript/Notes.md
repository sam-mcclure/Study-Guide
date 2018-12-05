# Week 1
## Prototypes

* If F has a prototype property with a value of the object type, then the new operator uses it to set [[Prototype]] for the new object

* Setting Rabbit.prototype = animal literally states that when a new Rabbit is created, assign its [[Prototype]] to animal

* Every function has the prototype property, even if we don't supply it. The default 'prototype' is an object with the only property constructor that points back to the function itself. We can use the constructor property to create a new obejct using the same constructor as the existing one

* JavaScript itself does not ensure the right 'contructor' value. Yes, it exists in the default prototype for functions, but that's all. What happens after is totally up to us. If we replace the default prototype as a whole, then there will be no constructor in it

* So, to keep the right 'constructor' we can choose to add/remove properties to the default 'prototype', instead of overwriting it as a whole

* The F.prototype property is not the same as [[Prototype]]. The only thing F.prototype does: it sets [[Prototype]] of new objects when new F() is called

* The value of F.prototype should be either an object or null: other values won't work

* The 'prototype' property only has such a special effect when it is set to a constructor function and invoked with new

* By default, all functions have F.prototype = { constructor: F}, so we can get the constructor of an object by accessing its 'constructor' property

## Closures

* **Closure** - The combination of a function and the lexical environment from which it was declared. Closure allows a function to access variables from an enclosing scope - environment - even after it leaves the scope in which it was declared

* The returned function can access variables from the enclosing scope

* It can refer to outer scope variables even after the outer function has returned

* One of the main benefits of closures is that it allows data encapsulation - the idea that some data should not be directly exposed

## Event Loop

* The heap is where memory allocation happens and the call stack is where the stack frames are

* WebAPIs are things that the browser provides, like DOM, Ajax, setTimeout etc

* JavaScript is a single threaded programming language. It has a single call stack and can only run one thing at a time.

* Callstack is a data structure that records where in the program we are. If we step into a function, we add something to the top of the stack. If we return from a function, we pop something off of the stack

* Things that are slow on the stack can block other functions

* You have to wait until the processes are done. If you're making a network request, this could be a long time

* Browser can't do anything/is stuck until first requests return.

* The solution? Asynchronous callbacks. You run code/a response and get a response later

* When a web API/ async action is finished, it gets pushed into the task queue.

* The event loop looks at the call stack and the task queue. If the stack is empty, it takes the first thing out of the task queue and pushes it onto the callstack to be executed

* If you want to defer something until the stack is clear, you can call setTimeout 0. This will push it into the task queue instead of the callstack

* All of the webAPIs/async callbacks work this way. They will get added to the task queue when completed

* setTimeout does not guarantee that the function returns in that time, rather that is the minimum possible time for the function to run. May need to wait for other actions in the task queue

* Render is given higher priority than other callbacks. It also has to wait for other actions to finish

## IIFE

* Immeadiately Invoked Function Expression. A function expression that is called immediately after you define it. It is usually used when you want to create a new variable scope

* The (surrounding parenthesis) prevernts it from treating it as a function declaration

* The final parenthesis() are executing the function expression

* On IIFE you are calling the function exactly when you are defining it( result.push( function() {return i}))

* Using IIFE enables you to attach private data to a function, creates fresh environments, and avoids polluting the global namespace

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