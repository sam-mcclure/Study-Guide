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

## Event bubbling

* Bubbling - When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.

* A handler on a parent element can always get the details about where it actually happened. 

* The most deeply nested element that caused the event is called a target element, accessible as event.target

* event.target is the 'target' element that initiated the event, it doesn't change through the bubbling process. 

* event.currentTarget or 'this' is the current element, the one that has a currently running handler on it

* A bubbling event goes from the target element straight up. Normally, it goes upwards until <html>, and then to the 'document' object, and some events even reach 'window', calling all handlers on the path.

* Any handler may use event.stopPropagation() to decide that the event has been fully processed and stop the bubbling

* event.stopPropogation() stops the move upwards, but on the current element all other handlers will run. If an element has multiple event handlers on a single event, then even if one of them stops the bubbling, the other ones will still execute. 

* To stop the bubbling and prevent handlers on the current element from running, there's a method called event.stopImmeadiatePropogation(). After it, no other handlers execute

* Bubbling is convenient. Don't stop it without a real need: obvious and architecturally well-thought.

* Sometimes, event.stopPropagation() creates hidden pitfalls that later may become problems. For instance:
    - We create a nested menu. Each submenu handles clicks on its elements and calls stopPropagation so that outer menus don't trigger
    - Later, we decide to catch clicks on the whole window, to track users's behavior (where people click). Some analytic systems do that. Usually, the code uses document.addEventListener('click') to catch all clicks
    - Our analytic won't work over the area where clicks are stopeed by stopPropagation. We've got a 'dead zone'

* There's usually no real need to prevent the bubbling. A task that seemingly requires that may be solved by other mean. One of them is to use custom events. Also, we can write our data into the event object in one handler and read it in another one, so we can pass to handlers on parents information about the procesing below.

* The standard DOM Events describes 3 phases of event propagation:
    1. Capturing Phase - the event goes down to the element
    2. Target phase - the event reached the target element
    3. Bubbling phase - the event bubbles up from the element

* The event first goes through the ancestors chaing down to the element (capturing), then it reaches the target, and then it goes up (bubbles), calling handlers on its way

* Before we only talked about bubbling, because the capturing phase is rarely used. Normally, it's invisible to us

* Handlers added using on<event> property or addEventListener don't know anything about capturing, they only run on the 2nd and 3rd phases

* To catch an event on the capturing phase, we need to set the 3rd argument of addEventListener to true.

* event.eventPhase will tell you the number of the phase on which the event was caught, but it's rarely used, because we usually know it in the handler

* When an event happens - the most nested element where it happens gets labeled as the 'target element' (event.target)

* Then, the event first moves from the document root down to the event.target, calling handlers assigned with addEventListener(..., true) on the way

* Then, the event moves from event.target up to the root, calling handlers assigned using on<event> and addEventListener without the 3rd arguement or with the 3rd argument false.

* Each handler can access event object properties: 
    - event.target: the deepest element that originated the event
    - event.currentTarget (=this) - the current element that handles the event (the one that has the handler on it)
    - event.eventPhase: the current phase (capturing=1, bubbling=3)

* Any event handler can stop the event by calling event.stopPropagation(), but that's not recommended because we can't really be sure we won't need it above, maybe for completely different reasons

* The capturing phase is used very rarely, usually we handle events on bubbling. 

* Bubbling and capturing lay the foundation for 'event delegation', an extremely powerful event handling pattern

## Event Delegation

* Capturing and bubbling allow us to implement one of the most powerful event handling patterns called event delegation.

* The idea is that if we have a lot of elements handled in a similar way, then instead of assigning a handler to each of them, we put a single handler on their common ancestor. In the handeler, we get event.target, see where the event actually happened, and handle it

* We can also use event delegation to add 'behaviors' to elements declaratively, with special attributes and classes. 

* The pattern has two parts:
1. We add a special attribute to an element
2. A document-wide handler tracks events, and if an event happens on an attributed element - performs an action

* When we assign an event handler to the document object, we should always use addEventListener, not document.onClick because the latter will cause conflicts: new handlers overwrite old ones

* Event delegation if often used to add the same handlers for many similar elements.

* The algorithm:
1. Put a single handler on the container
2. In the handler - check the source element event.target
3. If the event happened inside and element that interests us, then handle that event

* Benefits:
- Simplifies initalization and saves memory: no need to add many handlers
- Less code: when adding or removing elements, no need to add/remove handlers
- DOM modifications: we can mass add/remove elements with innerHTML and alike

* The delegation does have limitations:
- First, the event must be bubbling. Some events do not bubble. Also, low-level handlers should not use event.stopPropagation()
- Second, the delegation may add CPU load, because the container-level handler reacts on events in any place of the container, no matter if they interest us or not. But usually, the load is negligible, so we don't take that into account

## ES5 vs ES6

* ECMAScript 6 (ES6) features can be divided into features that are pure syntactic sugar (like class), features that enhance JavaScript (like import), and features that fix some of JavaScript's bad parts (like the let keyword).

* Block Scope - ES5 only had function-level scope (you wrap code in functions to create scope) and caused a lot of issues. ES6 provides 'block'-level scoping (ie curly-braces to scope) when we use 'let' or 'const' instead of 'var'

* Some benefits of block scope:
- Prevent variable hoisting outside of scope ('let' and 'const' do not hoist)

- Prevent duplicate variable declaration (ES6 doesn't allow duplicate declaration of variables when we declare them using 'let' or 'const in the same scope. This is helpful to avoid duplicate function expressions coming from different libraries)

- Eliminates the need for IIFE (In ES5, we had to use IIFE to ensure we don't pollute or overwrite the global scope. In ES6, we can just use curly braces and use const or let to get the same effect)

- babel - A Tool to convert ES6 to ES5 (You ultimately need to run ES6 in a regular browser. Babel is the most popular tool used to convert ES6 to ES5)

- Makes it trivial to use functions in loops (In ES5, if you had a function inside a loop, if that function tried to access the looping variable 'i', i would get hoisted as a global variable. In ES6, you
 can use 'let' and use functions without any issue)

 * Lexical 'this' (via arrow functions) - In ES5, 'this' can vary based on where it is called and even how it is called and can cause problems. ES6 eliminates this major issue by using a lexical this.

 * Lexical 'this' is a feature that forces the variable 'this' to always point to the object where it is physically located within. You get lexical this automatically by using the fat-arrow function => 

 * Dealing with 'arguments' - In ES5, 'arguments' acts like an array (ie you can loop over it), but it's not an array so functions like sort and slice etc are not available. 
 
 * In ES6, you can use a new feature called 'Rest' parameters. It's represented with 3 dots and a name, like ...args. Rest parameteres is an array, so we can use all array functions.

 * Classes - there is no such thing as a 'class' in JS like it is in other OO langauges. But people have treated the function constructors that create objects when you use the 'new' keyword as classes.

 * Since JS doesn't support the classes and just simulates it via prototypes, it's syntax has been confusing for JS developers who want to use it in a traditional OO fashion. This is especially true for things like creating subclasses, calling functions in parent classes and so on

 * ES6 brings a new syntax that's common in various programming languages and amkes the whole thing simple. It allows a class keyword that looks and functions more similarly to OO languages

 * Strict mode - 'use strict' helps identify common issues and also helps with securing JavaScript. In ES5, the strict mode is optional, but in ES6, it's needed for many ES6 features, so most people and tools like babel automatically add 'use strict' at the top of the file, putting the whole JS code in strict mode and forcing us to write better JavaScript

 ## Error Handling

 * Sometimes scripts have errors. They may occur because of programmer mistakes, unexpected user input, an erroneous server response, or thousands of other reasons.

 * Usually, a script immeadiately stops in case of an error, printing it to the console

 * 'try..catch' allows us to 'catch' errors and, instead of stopping the script, do something more reasonable

 * The 'try..catch' construct has two main blocks: 'try', then 'catch':

 ```JS
 try{
     // code
 } catch (err) {
     // error handling
 }
 ```

 * First, the code in 'try {...}' is executed. If there were no errors, then 'catch(err)' is ignored: the execution reaches the end of try and then jumps over catch. If an error occurs, then 'try' execution is stopped and the control flows to the beginning of 'catch(err)'. The 'err' variable contains an error object with details about what's happened.

 * So, an error inside the try block does not kill the script, we have a chance to handle it in catch

 * 'try..catch' only works for runtime errors. For 'try..catch' to work, the code must be runnable. In other words, it should be valid JavaScript (it won't work if the code is syntactically wrong)

 * Errors that occur in the reading phase are 'parse-time' errors and are unrecoverable(from inside that code).

 * 'try..catch' works synchronously. If an exception happens in 'scheduled' code, like in setTimeout, then 'try..catch' won't catch it. That's because try..catch actually wraps the setTimeout call that schedules the function. But, the function itself is executed late, when the engine has already left the 'try..catch' constuct.

 * To catch an exception inside a scheduled function, try..catch must be inside that function

 * When an error occurs, JavaScript generates an object containing the details about it. The object is then passed as an argument to catch.

 * For all built-in errors, the error object inside the 'catch' block has two main properties: name (error name, for an undefined variable that's 'reference error) and message (textual message about error details)

 * There are other non-standard properties available in most environments. One of the most widely used and supported is stack (current call stack, a string with info about the sequence of nested calls that led to the error)

 * The 'throw' operator generates an error. The syntax is: throw <error object>

 * Technically we can use anything as an error object, but it's better to use obejcts with name and message properties (to stay compatible with built-in errors)

 * JavaScript has built in constructors for standard errors, such as Error, SyntaxError, ReferenceError, and TypeError. We can invoke these like let error = new Error(message);

 * Catch should only process errors that it knows and 'rethrow' all others.

 * The 'rethrowing' technique can be explained as:
 1. Catch gets all errors
 2. In the catch(err) {...} block, we analyze the error object err
 3. If we don't know how to handle it, then we do throw error

 * try..catch may have one more code clause: finally. If it exists, it runs in all cases (after catch if there were no errors and after catch if there were errors)

 ```JS
 try {
     //try to execute the code
 } catch(e) {
     //handle errors
 } finally {
     //execute always
 }

 ```

 * The finally clause if often used when we start doing something before try..catch and want to finalize it in any case of outcome. 

 * The finally clause works for any exit from try..catch, including explicit return

 * The try..finally construct, without catch clause, is also useful. We apply it when we don't want to handle errors right here, but want to be sure that processes that we started are finalized

 * The role of the global handler window.onerror is usually not to recover the script execution, but to send the error messages to developers. 

 * The try..catch construct allows us to handle runtime errors. It allows us to try running the code and catch errors that may occur in it.

 * There may be no catch section or no finally, so try..catch and try..finally are also valid.

 * Error objects have the following properties:
 - message: the human-readable error message
 - name: the string with error name (error constructor name)
 - stack (non-standard): the stack at the moment of error creation

 * We can also generate our own errors using the throw operator. Technically, the argument of throw can be anything, but it's usually an error object inheriting from the built-in error class

 * Rethrowing is a pattern of error handling: a catch block usually expects and knows how to handle a particular error type, so it should rethrow errors it doesn't know.
 
 * Even if we don't have 'try..catch', most environments allow you to set up a 'global' error handler to catch errors that fall out. In-browser, that's window.onerror

 ## Custom Errors

 * When you develop something, you often need your own error classes to reflect specific things that may go wrong in your tasks. For network operations, you may need HttpError, for database operations DbError, for searching operations NotFoundError, and so on.

 * Your errors should support basic error properties like message, name, and stack. They also might have properties of their own, like statusCode.

 * JavaScript allows us to use throw with any argument, so technically our custom error classes don't need to inherit from error, but if we do, it becomes possible to use obj instanceof Error.

 * As you build your application, your own errors naturally form a heirarchy, for instance HttpTimeoutError may inherit from HttpError, and so on

 ```JS
 //pseudocode for built in Error class
 class Error {
     constructor(message) {
         this.message = message;
         this.name = "Error";
         this.stack = <nested calls/>;
     }
 }

  class ValidationError extends Error {
      constructor(message){
          super(message);
          this.name = "ValidationError";
      }
  }
 ```

 * We can inerit from Error and other built-in error classes normally, we just need to take care of the name property and call super

 * Most of the time, we should use instanceof to check for particular errors. It also works with inheritance. But sometimes we have an error object coming from a 3rd-party library and there's no easy way to get the class. Then, the name propery can be used for such checks.

 * Wrapping exceptions is a widespread technique when a function handles low-level exceptions and makes a higher-level object to report about the errors. Low-level exceptions sometimes become properties of that object, like err.cause, but that's not strictly required.