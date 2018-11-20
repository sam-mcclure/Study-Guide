# Prototypes

* If F has a prototype property with a value of the object type, then the new operator uses it to set [[Prototype]] for the new object

* Setting Rabbit.prototype = animal literally states that when a new Rabbit is created, assign its [[Prototype]] to animal

* Every function has the prototype property, even if we don't supply it. The default 'prototype' is an object with the only property constructor that points back to the function itself. We can use the constructor property to create a new obejct using the same constructor as the existing one

* JavaScript itself does not ensure the right 'contructor' value. Yes, it exists in the default prototype for functions, but that's all. What happens after is totally up to us. If we replace the default prototype as a whole, then there will be no constructor in it

* So, to keep the right 'constructor' we can choose to add/remove properties to the default 'prototype', instead of overwriting it as a whole

* The F.prototype property is not the same as [[Prototype]]. The only thing F.prototype does: it sets [[Prototype]] of new objects when new F() is called

* The value of F.prototype should be either an object or null: other values won't work

* The 'prototype' property only has such a special effect when it is set to a constructor function and invoked with new

* By default, all functions have F.prototype = { constructor: F}, so we can get the constructor of an object by accessing its 'constructor' property

# Closures

* **Closure** - The combination of a function and the lexical environment from which it was declared. Closure allows a function to access variables from an enclosing scope - environment - even after it leaves the scope in which it was declared

* The returned function can access variables from the enclosing scope

* It can refer to outer scope variables even after the outer function has returned

* One of the main benefits of closures is that it allows data encapsulation - the idea that some data should not be directly exposed