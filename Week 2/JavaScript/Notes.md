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