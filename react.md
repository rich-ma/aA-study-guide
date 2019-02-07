# React Notes
## Intro to JSX
- React is a JS library made by FB
- React is fast, modular, scalable, flexible, popular
- JSX is syntactic sugar for javascript made to be used with React.
- JS code with JSX in it needs to be compiled and translated into JS.
- basic unit of JSX is a JSX element.looks like html
- ex
```javascript
  <h1>Hello world</h1>
```
- JSX elements are treated as JS, can go anywhere that JS expressions can go
  - can be saved in a variable, passed to a function, stored in an object or array

### JSX Attributes
- JSX elements can have attributes, like HTML elements
- JSX attribute is written using HTML-like syntax with a name and a value stored in quotes
- ex:
```javascript
<a href="http://www.example.com">Welcome to the Web</a>;

const title = <h1 id="title">Introduction to React.js: Part I</h1>;
```
- the anchor tag <a> has a href attribute, and the object title has a id attribute.
  - elements can have multiple attributes like in html as well.

### Nested JSX
- can nest JSX elements inside of other elements like HTML
- ex:
```javascript
<a href="https://www.example.com">
  <h1>
    Click me!
  </h1>
</a>
```
- this ex has a h1 tag nested inside of an achor tag.
- if a JSX expression takes up more than 1 line, you must wrap the multi-line in parentheses
- JSX has **At Most** One outermost element, needs to have 1 parent element with others nested, can't have two elements at the same level.

## Rendering JSX
- need to import React, and ReactDOM
- Both of these are libraries, ReactDOM contains React specific methods, dealing with the DOM(Document Object Model)
- ReactDOM.render is a method that renders JSX, takes a JSX expression, creates a DOM node tree, and adds that tree to the DOM.
- The second argument is where you want the first JSX expression to appear.
- The first argument is appended to the second argument.


### Passing variables to ReactDOM.render()
- render's first arugment should evaluate to a JSX expression, doesnt have to literally be one
- nice thing about render() is that it only udpates DOM elements that have changed
- meaning if you render the exact thing twice in a row, the second render will do nothing
  - this is why REACT is so popular, using the virtual DOM to render
  - Virtual DOM is much faster than real DOM
- When you render a JSX element, every virtual DOM is updated, which sounds inefficient, but it is so fast and the cost in insignificant.
- Once the virtual DOM updates, React compares it to the previous snapshot and sees which objects have updated, this is called **diffing**.
- react will only update those components that have updated on the real DOM.  

When you update the DOM in React:
1. The entire virtual DOM gets updated.
2. The virtual DOM gets compared to what it looked like before you updated it. React figures out which objects have changed.
3. The changed objects, and the changed objects only, get updated on the real DOM.
4. Changes on the real DOM cause the screen to change.

# Advanced JSX

## self closing tags
  - in HTML its ok to put the forward slash before the closing angle bracket <br />, but <br> is also ok
- In JSX you **must** have the slash or you will have an error, <br />

## JS in your JSX
- use {} to wrap your JS code in JSX.
- {} are markers to signal the beginning and end of a **JS injection**

## variables in JSX
- When you inject JS into JSX, you have access to the environment in the rest of your file, meaning you can use variables available in that scope
- It is common to use an objects properties as attributes for JSX elements
```javascript
const pics = {
  panda: "http://bit.ly/1Tqltv5",
  owl: "http://bit.ly/1XGtkM3",
  owlCat: "http://bit.ly/1Upbczi"
}; 

const panda = (
  <img 
    src={pics.panda} 
    alt="Lazy Panda" />
);

const owl = (
  <img 
    src={pics.owl} 
    alt="Unimpressed Owl" />
);

const owlCat = (
  <img 
    src={pics.owlCat} 
    alt="Ghastly Abomination" />
);
```
### event listeners
- just like html, JSX can have event listeners
- <img onClick={myFunc} />
- the event listeners attribute value must be a function to work correctly

### conditionals
- cannot inject if statements into JSX
- has to do with how JSX is compiled
- you can write an if statement, and not inject it into JSX
- write the if statement outside, and create the conditional objects or changes within JS, and render that in JSX.
- Can use ternary operator in JSX.
- works the same way as JS.
- ex
```javascript
const headline = (
  <h1>
    { age >= drinkingAge ? 'Buy Drink' : 'Do Teen Stuff' }
  </h1>
);
```
- Can also use **&&** to conditionally render
- ex:
```javascript
const tasty = (
  <ul>
    <li>Applesauce</li>
    { !baby && <li>Pizza</li> }
    { age > 15 && <li>Brussels Sprouts</li> }
    { age > 20 && <li>Oysters</li> }
    { age > 25 && <li>Grappa</li> }
  </ul>
);
```

## .map in jsx
- can use map, already did this for lists, 
- can start with an array and map over it and creating li's, or any type of html tag you want
ex:
```javascript
const strings = ['Home', 'Shop', 'About Me'];

const listItems = strings.map(string => <li>{string}</li>);

<ul>{listItems}</ul>
```

### Keys
- key is a JSX attribute, need to to differentiate between different elements
- React uses these to keep track of lists, if you dont use keys, React might scramble your list-items into the wrong order
  - Usually use the item's ID, which is unique to the item, can also use the index
- A list needs key if either of the following are true:
  1. The list-items have memory from one rendering to the next, meaning they carry information from render to render, like a checklist
  2. a List's order might be shuffled, a list of search results might shuffle from render to render.

## React.createElement
- JSX is shorthand for using React.createElement

```javascript
const h1 = React.createElement(
  "h1",
  null,
  "Hello, world"
);
```
is the same as 
```javascript
const h1 = <h1>Hello world</h1>;
```
- createElement takes 3 arguments
  1. type
  2. props
  3. children

# React Components
- react components are small reusable chunks of code that is responsible for doing one job(rendering part of screen)
- always hve to import React from 'react';
  - creates a new variable called React
  - gives us methods from the **React Library**

## ReactDOM
- importing ReactDOM allows us to use ReactDOM methods, which interact with the virtual and real DOM

## Component Classes
- Every component must come from a component class
- these are like factory methods that create components
  - can use these classes to produce as many components as you want
- to make a component class, you use a base class from the React Library
  - **React.Component**
- React.Component is a JS class, need to subclass it by **extending** it
```javascript
class YourComponentNameGoesHere extends React.Component {}
```
- Component classnames **MUST START WITH A CAPITAL**, in UpperCamelCase

### render()
- component classes are like factory functions that build components  
- the render method is a function that must contain a return statement

## Creating Component Instances
- after your class has a render, you can use it as a working component class
```javascript
<MyComponentClass />
```
- You write a JSX element, and instead of giving it a standard HTML tag, you call it the classname
- When you make a component <MyComponentClass />, that component inherits all the methods of its component class


# ReactJS part 1

## Use variable attributes in a component
- can use interpolated data using {} in JSX

using conditionals
```javascript 
import React from 'react';
import ReactDOM from 'react-dom';

class TodaysPlan extends React.Component {
  render() {
    let task;
    if (!apocalypse) {
      task = 'learn React.js'
    } else {
      task = 'run around'
    }

    return <h1>Today I am going to {task}!</h1>;
  }
}

ReactDOM.render(
	<TodaysPlan />,
	document.getElementById('app')
);
```
- change what **task** represents conditionally

## using This in a component
- this represents the instance of the component that you are in
```javascript
class IceCreamGuy extends React.Component {
  get food() {
    return 'ice cream';
  }

  render() {
    return <h1>I like {this.food}.</h1>;
  }
}
```
- this would be an instance of IceCreamGuy, could be something else, but usually the object

## Using event listeners in components
- event handlers are functions that get called in response to an event
- ex:
```javascript
class MyClass extends React.Component {
  myFunc() {
    alert('Stop it.  Stop hovering.');
  }

  render() {
    return (
      <div onHover={this.myFunc}>
      </div>
    );
  }
}
```

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

class Contact extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      password: 'swordfish',
      authorized: false
    };
    this.authorize = this.authorize.bind(this);
  }

  authorize(e) {
    const password = e.target.querySelector(
      'input[type="password"]').value;
    const auth = password == this.state.password;
    this.setState({
      authorized: auth
    });
  }

  render() {
    const login = (
    	<form action="#" onSubmit=>
      	<input type="password" placeholder="Password" />
      
      	<input type='submit' />
      </form>
    );
    
    const unauthorized = (
        <div>
        <h1>Enter the Password</h1>
      	{login}
        </div>
      );
    
    const contactInfo = (
        <div>
          <h1>Contact</h1>
          <ul>
            <li>
              client@example.com
            </li>
            <li>
              555.555.5555
            </li>
          </ul>
        </div>
      );
    
    return (
      <div id="authorization">
       { this.state.authorized ? contactInfo : unauthorized }
      </div>
    );
  }
}

ReactDOM.render(
  <Contact />, 
  document.getElementById('app')
);
```