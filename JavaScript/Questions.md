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