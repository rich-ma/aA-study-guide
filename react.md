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