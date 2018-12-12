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

## == vs ===

* == checks for eqaulity with coercion and === checks for equality without coercion - strict equality
- 2 == '2' True, 2 === '2' False

* If you are comparing a boolean with something other than a boolean, JavaScript coerces that boolean to a number and compares. This comparison is now between a number and a string. Javascript now coerces that string to a number and compares both numbers. 

- false == "" true, false == [] true, false == {} false,
"" == 0 true, "" == [] true, "" == {} false, 0 == [] true,
0 == {} false, 0 == null false

## this

* Functions that are stored in object properties are called 'methods'

* Methods allow objects to 'act' like object.doSomething()

* Methods can reference the object as 'this'

* The value of 'this' is defined at run-time

* When a function is declared, it may use 'this', but that 'this' have no value until the function is called

* That function can be copied between objects

* When a function is called in the 'method' syntax object.method(), the value of 'this' during the call is 'object'

* Arrow functions are special: they have no 'this'. When 'this' is accessed inside an arrow function, it is taken from outside.

* Objects are usually created to represent entitites of the real world, like users and so on. Actions are represented in JavaScript by functions in properties

* A function that is the property of an object (defined on the object like user.sayHi = function) is called its method

* There exists a shorter syntax for methods in an object literal:
```JS
let user = {
    sayHi () { //same as user.sayHi
        alert("Hello");
    }
}
```

* This shorter syntax is usually preferred

* It's common that an object method needs to access the information stored in the object to do its job. To access the object, a method can use the 'this' keyword. The value of 'this' is the object 'before dot', the one used to call the method. 

* In JavaScript, 'this' keyword behaves unlike most other programming languages. First, it can be used in any function. The value of 'this' is evaluated during run-time and it can be anything

* If you try to use the function without an object, 'this' will be undefined in strict mode. If you try to access this.name, there will be an error. In non-strict mode (if you forget 'use strict') the value of 'this' in such case will be the global object (window). This is a historical behavior that 'use strict' fixes.

* Usually a call of a function that uses 'this' without an object is not normal, but rather a programming mistake. If a function has 'this', then it is usually meant to be called in the context of an object

* In JavaScript, 'this' is free, its value is evaluated at call-time and does not depend on where the method was declared, but rather on what's the object before the dot. On one hand, the function can be reused for different objects. On the other, greater flexibility opens the door for mistakes. 

* First, the dot retrieves the property obj.method. Then, parentheses () execute it. If we put these operations on separate lines, 'this' will be lost

* To make user.hi() calls work, JavaScript uses a trick - the dot returns not a function, but a value of the special Reference Type. The Reference Type is a 'specification' type. We can't explicitly use it, but it is used internally by the language.

* The value of Reference Type is a three-value combination (base, name, strict) where base is the object, name is the property, and strict is true is use strict is in effect. When parentheses are called on the Reference Type, they receive the full information about the object and its method, and can set the right 'this'. Any other assignment discards the Reference Type.

* 'this' is only passed the right way if the function is called directly using a dot obj.method() or square brackets obj['method']()

* Arrow functions are special, they don't have their own 'this'. If we reference 'this' from such a function, it's taken from the outer 'normal' function.