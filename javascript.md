# Javascript notes
---


# Franziska Hinkelmann: JavaScript engines - how do they even? | JSConf EU 2017

![jsvideo](https://www.youtube.com/watch?v=p-iiEDtpy6I)
- EcmaScript Standard decided by TC39
- V8 is google chrome JS engine
- engine uses rules and standards and runs javascript

- if you write JS code, dont have to type your variables
- dont have to worry about different types of ints, like you do in other languages
  - language is dynamically typed, not statically typed
- can add and delete properties to an object easily, and from a prototype 
- compilers need to know type, to be able to make machine code quickly and compile it into an executabl


# Prototype
- Prototypes are a fundamental feature of Javascript. Given this topic's importance to the language, they are a very hot interview/phone screen topic. Having a strong grasp on Javascript Prototypes will give you a major leg-up in the application process.
- We can use __proto__ to determine an objects prototype now, but didn't used to be able to
- JS has prototypal inheritance from the beginning, core feature of JS.
- but before we had to use the "prototype" property of the constructor function.
  
## The prototype property
- new F(), creates a new object, the objects prototype is set to F.prototype;
- if F has a prototype property with value of the object type, new operator sets it to [[Prototype]] for the new object.
- F.prototype means a reguar property names prototype on F.

```javascript
let animal = {
  eats: true
};

function Rabbit(name) {
  this.name = name;
}

Rabbit.prototype = animal;

let rabbit = new Rabbit("White Rabbit"); //  rabbit.__proto__ == animal

alert( rabbit.eats ); // true
```
- in this code, we create this animal object, and set the prototype of the constructor Rabbit to animal, meaning anything created using this constructor will have this prototype of animal.

## Default F.prototype contructor property
- Every function has a prototype by default, the default prototype is an object with the property 'constructor' that points back to the function.
- function Rabbit(){}
- Rabbit.prototype.constructor = Rabbit();
- We can use the constructor property of an object to create a new object of that type.
  - useful for when we have an object and dont know exactly what constructor was used to create it.
- Javascript does not esnure the right "constructor" value
  - if you replace the default prototype, the constructor will be gone all together
  - in order to fix this, we can modify the actualy prototype, instead of rewriting it.
  - Rabbit.prototype.jumps = true
  - or we can replace the prototype and recreate the constructor correctly
```javascript
Rabbit.prototype = {
  jumps: true,
  constructor: Rabbit
};
```

## Summary
- F.prototype is not the same as [[Prototype]], it sets the [[Prototype]] of a new ojbect when new F() is called.
- F.prototype should either be an object or null
- prototype property only has this special effect when it is set to a constructor and invoked using 'new'
