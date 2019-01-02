# Javascript notes
---

# Try, catch, finally, Error Handling
- try is the first step in error handling, used as first step in code that is likely to fail
- usually followed by:
  - try-catch
  - try-finally
  - try-catch-finally
- **catch** directly follows the try block, and is executed only if a exception is thrown
  - contains statements on what to do if an exception is thrown
  - if no exception is caught in the try block, the catch will be **skipped**
  - if any statement within the try block(including external function calls) throw an exception, the catch clause will take control.
- **finally** block goes fater the try-catch block, and **always** executes regardless of any exceptions

Example:
```javascript
function getElement(arr, pos) {
    return arr[pos];
}


//let arr = [1, 2, 3, 4, 5];

try {
    console.log(getElement(arr, 4));
} 
catch (e) {
    console.log(e.message);
}
console.log("The program continued executing!");
```
- in this code, the catch block will execute because **arr** does not exist, and will print the error message.

```javascript
//let arr = [1, 2, 3, 4, 5];

try {
    console.log(getElement(arr, 4));
} 
finally {
    console.log("Finally Block");
}
console.log("The program continued executing!");
```
- in this code, the console will not log "The program continued executing!" because there was never a catch, and the code terminated after the finally block(Which always runs regardless of exceptions or not)

```javascript
"use strict";

const arr = [1, 4, 3, 4, 5];

try {
    arr = [4, 2];
    console.log(arr.sort());
} 
catch (e) {
    console.log(e.message);
} 
finally {
    console.log(arr.sort());
}
```
- in this code, we can't reassign the const arr, so they catch will log, but the finally will still log arr.sort();

## throw
- we use throw to an exception, can use a custom error, or throw some value
- in the example below, functions containing throw statements are called from within the try blocks and is caught with the catch block
```javascript
function throwString() {
    // Generate an exception with a String value
    throw "some exception";
}

function throwFalse() {
    // Generate an exception with a boolean value of false
    throw false;
}

function throwNumber() {
    // Generate an exception with a Number value of -1
    throw -1;
}

try {
    throwString();
}
catch (e) {
    console.log(e);
}

try {
    throwFalse();
}
catch (e) {
    console.log(e);
}

try {
    throwNumber();
}
catch (e) {
    console.log(e);
}
```
- output: 'some exception', false, -1

### custom errors
- throw new Error(input);
- this allows us to customize the error message that is thrown to the catch block, allowing us to customize the response that the user encounters
- 


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



# Javascript Closures
- a combination of a function and the lexical enviroment where it was declared
- allow a function to wrap over the variables from the enclosing scope-environment-
- it even has access to the variables after leaving the scope where it was declared
```javascript

function sayHi(name){
  var message = `Hi ${name}!`;
  function greeting() {
    console.log(message)
  }
  return greeting
}
var sayHiToJon = sayHi('Jon');
console.log(sayHiToJon)     // ƒ() { console.log(message) }
console.log(sayHiToJon())   // 'Hi Jon!'
```
- in this code, the greeting function has access to the message outside of its scope, due to closing over it
- will correctly log the argument passed to the function
- The above example covers the two things you need to know about closures:
- Refers to variables in outer scope.
- The returned function access themessage variable from the enclosing scope.
- It can refer to outer scope variables even after the outer function has returned. 
- SayHiToJon is a reference to the greeting function, created when sayHi was run. The greeting function maintains a reference to its outer scope — environment — in which message exists.


- Closures allow for Data Encapsulation, meaning that it protects data that should not be exposed
```javascript
function SpringfieldSchool() {
  let staff = ['Seymour Skinner', 'Edna Krabappel'];
  return {
    getStaff: function() { console.log(staff) },
    addStaff: function(name) { staff.push(name) }
  }
}

let elementary = SpringfieldSchool()
console.log(elementary)        // { getStaff: ƒ, addStaff: ƒ }
console.log(staff)             // ReferenceError: staff is not defined
/* Closure allows access to the staff variable */
elementary.getStaff()          // ["Seymour Skinner", "Edna Krabappel"]
elementary.addStaff('Otto Mann')
elementary.getStaff()          // ["Seymour Skinner", "Edna Krabappel", "Otto Mann"]
```
- in this example, when elementary is created, the outer function is already returned, and staff only existed inside the closure
- gives you access to get staff still, and addStaff, but staff itself is protected.


Ex questions
what is wrong with this code?
```javascript
const arr = [10, 12, 15, 21];
for (var i = 0; i < arr.length; i++) {
  setTimeout(function() {
    console.log(`The value ${arr[i]} is at index: ${i}`);
  }, (i+1) * 1000);
}
```
- since there is a set timeout, the timeout function will not run until everythign else is done
- this means that i=4 at this point, and we will get an error that arr[4] does not exist
- we can fix this by using IIFE(Immediately-invoked function expression) pronounced Iffy
  - coding pattern that allows functions to be called immediately, instead of waiting on the regular javascript
```javascript
const arr = [10, 12, 15, 21];
for (var i = 0; i < arr.length; i++) {
  (function(j) {
    setTimeout(function() {
      console.log(`The value ${arr[j]} is at index: ${j}`);
    }, j * 1000);
  })(i)
}
```
- in this code, we write a for loop, looping over the array, and creating an anonymous function that we call immediately(IFFY immediately-invoked function expression)
- we create this variable 'j' in each fucntion call, which stores the value 'i' from the outer function, meaning that it will hold onto the value through the event loop.

- can also fix this by using a let instead of a var in the for loop
```javascript
for (let i = 0; i < arr.length; i++) {
  setTimeout(function() {
    console.log(`The value ${arr[i]} is at index: ${i}`);
  }, (i) * 1000);
}
```
- this works because of the **scope** difference between let and var.
  - the value of i in the var is locked to the outer scope(nearest function block) in which the function was called( i = 4)
  - while the value of i in the let example, the value of i is scoped to the nearest enclosing block, meaning it maintains the value of i by declaring it within the enclosing scope.
  - 


# Javascript callstack, concurrency, event loop
- javascript is a single threaded non-blocking asynchronous, concurrent langauge
- has calls tack, event loop, callback queue, and other apis
- JS call stack functions like a regular call stack, LIFO(last in, first out)
![callstack](callstack.jpg)

- blocking
  - code that is slow, console.log is fast, network requests slow, etc
  - blocking is an issue becuase it locks you out from being able to do anything on the web.
    - big issue, which is why we are given concurrency and event loop

- Asychronous requests
  - code gets stuck, can't do other things until others are done
  - simplest solution is asychronous callbacks
    - run the code later after everything else is done
  - set timeout gets put on the stack, but just disappears, goes to event loop
  ![asych](asych_call.jpg)

## Concurrency and Event Loop
- Where does the settimeout go after the stack?
- JS lets us do concurrency since browser can do more than just the JS runtime(which can only do 1 thing at a time)
- browser gives us WebAPIs that let us access like threads, and where concurrency happens
- threading is hidden, run somewhere else
- setTimeOut gets called, goes on the stack, then goes to the API call for setTimeOut(External API)
![concurr1](concurr1.jpg)
- then browser will set the countdown for you, and since it is done, it will remove itself from the stack.
![concurr2](concurr2.jpg)
- now rest of code can be called, (console.log('JSConfEU')) 
- after the asynch call is done(setTimeOut), it will enter the queue(task queue), and wait for the stack to clear until it will be called
![concurr3](concurr3.jpg)

## Event Loop
- one job, look at the stack, and the stack queue
- if stack is empty, it will grab the first thing in the queue(first in first out, FIFO)
- now that stack is clear, will move the callbck to the js stack, and in this case, will call the console.log('there'), and put that on the stack as well
![concurr4](concurr4.jpg)


### ex. SetTimeOut(0)
- if you want to defer sometime until stack clears, use a time of 0 for setTimeOut, will complete immediately, but dont happen until the normal stack clears.
- setTimeOut isnt gaurantee to run in that time, that is the minimum time it will take to complete.

callback:
- any function that another function calls
- can be an asychnronous callback, that will be pushed onto callback queue in the future.
- by using asych we are able to not block the call stack, otherwise the browser will be 'blocked up' and unable to repaint, or allow user interactions.
- by using asynch we can give the browser a chance to repaint between event loop.

- can also flood the callback queue, only do slow work every few seconds, or until user stops scrolling, not during all user inputs.