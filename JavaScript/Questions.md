# Prototypes

1. Give a high level overview of what an object's prototype represents
- When an object is created, a second object called a prototype is created. This prototype allows for object or 'class' inheritance. By defining attributes or methods on an object's prototype, you can use the new keyword to create another obeject with the same attributes and methods, fetched from the prototype

2. What are the differences between the __proto__ and prototype attributes?
- O's prototype is used to establish the prototype of objects created by calling new O(). O.__proto__ is a nonstandard mechanism for retrieving an object's prototype object. The prototype is what gets applied to a new object, __proto__ is used to find what the prototype of an object is

3. What happens when we do or don't explicity set an object's prototype?
- If you don't set an object's prototype, it defaults to a constuctor that points to the object. If you overwrite an object's prototype, the constructor will be removed unless you declare a new one. By adding to a prototype, you can declare methods and attributes that will be attached to instances of the object

4. What is an object's default prototype?
- F.prototype = { constructor: F}

5. What are the valid values for an object's prototype?
- Object or null

# Closures

6. What are the benefits of a Javascript closure?
- Closures allows a function to access variables from an enclosing scope - environment - even after it leaves the scope in which it was declared. They allow data encapsulation - the idea that some data should not be directly exposed to the user

7. Formally define a Javascript closure
- The combination of a function and the lexical environment from which it was declared.

8. Give an example of a closure
```js
function sandwichMaker(mainIngredient){
    return function(filling){
        return mainIngredient + "and" filling;
    };
}
```

9. What is data encapsulation?
- Data encapsulation is the idea that some data should not be directly exposed to a user

# Event Loop

10.  What is the difference between the memory heap and call stack in javascript?
- The memory heap is where memory allocation happens. The call stack is were stack frames are/where you store and execute actions

11. What is one problem with programming languages that are fully single-threaded?
- Single a single-threaded language can only execute one action at a time, if an action takes a long time to finish, all other actions will have to wait for it and the browser can get stuck