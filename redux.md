# redux notes, Dan Abramov
- Dan Abramov, the creator of Redux
- state management notes
- Redux offers a mature solution to managing state in React Apps.
- By using a few useful patterns, Redux is able to organize your application using JS.

## 1. Single Immutable State Tree
- all state changes in Redux are explicit
- everything that changes in the App is contained in a single object called the **state** or **state tree**
- ex. state:
```javascript 
"current_state:"
[object Object] {
  todos: [[object Object] {
    completed: true,
    id: 0,
    text: "hey",
  }, [object Object] {
    completed: false,
    id: 1,
    text: "ho",
  }],
  visibilityFilter: "SHOW_ACTIVE"
}
```
## 2. Describing State changes with actions
- The state tree is read only.  You cannot modify or write to it.
- Must dispatch **actions**, minimal representations to the change to the data.
- Actions must have **type** that should be strings since they are serializable
- app with have different types of actions(login, receiveUsers, deleteUsers, addCounter, removeCounter)
- Actions scale well to medium and complex applications
- ex from disunity:
```javascript
export const LOGGED_IN = "LOGGED_IN";
export const LOGGED_OUT = "LOGGED_OUT";

export const userLoggedIn = id => ({
  type: LOGGED_IN,
  userId: id
});

export const userLoggedOut = id => ({
  type: LOGGED_OUT,
  userId: id
});
```

## 3. Pure and Impure functions
- **pure functions** are those whose return values depend only upon the value of their arugments.
  - don't have side effects like network or database calls.
  - don't override the values of anything, example below a new array is returned instead of modying the argument that was passed to it.
  - are predictable, if you call it the same way, should have the same return
```javascript
function square(x) {
  return x * x;
}
function squareAll(items) {
  return items.map(square);
}
```

- **impure functions** have network or database calls. 
- values passed in are overwritten, Redux requires that certain functions are Pure, should not modify them, but some require to be impure.
- 
```javascript
function square(x) {
  updateXInDatabase(x);
  return x * x;
}
function squareAll(items) {
  for (let i = 0; i < items.length; i++) {
    items[i] = square(items[i]);
  }
}
```

## 4. Reducer function
- UI is most predictable when it is described as a pure function of the applications state.
- Reducer functions take the current state and the new action being dispatched and returns the next state of your function
- important that it doesn't modify the state given to it(const newState = merge({}, state);)
- reducers must be pure functions that do not modify the original state, and return a new slice of state.
- inside any redux app, 

## 5. Writing a counter reducer with Tests
- need to default a current state of the application if the reducer receives an action that is unknown/it is not responsible for.
  - should return the initial state;
- if state is not defined, return an object representing the original state
```javascript
const counter = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}
```
- uses a switch statement, with a default that will return the original state, and corresponding reducer actions for actions that it has the **type** for.


## 6. Store Methods: getState(), dispatch(), and subscribe()
- bringing 
```javascript
// import { createStore } from 'redux' // npm module syntax

const { createStore } = Redux; // Redux CDN import syntax
const store = createStore(counter);
```
- store binds together three principles of Redux
  1. Holds the current application state object
  2. Allows you to dispatch actions
  3. when you create it, you need to specify the reducer that tells how sate is updated with actions
- in this example we call createSTore with counter as the reducer that manages the state updates.

1. getState();
   - retrieves current state of redux store. 
2. dispatch();
   - lets you dispatch actions to update the state of your app.
   - is the most commonly used.
3. subscribe();
   - registers a callback that the redux store will callany time an action has been dispatched, so you can update the UI of your app to reflect the current application state.e

ex.
```javascript
const counter = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}

import { createStore } from 'redux';

const store = createStore(counter);
//takes counter as an argument for 

```
- createStore takes 3 arguments, createStore(reducer, preloadedState, enhancer)
  - **reducer(function)**: a reducing function that returns the next state tree, given the current state tree and an action to handle
  - **preloaded state**: the initial state, can hydrate the state from the server in a universal app, or restore prev. serialzed user session/
    - if you use combineReducers, you need to give a preloaded state with the same shape as the keys passed to it.
  - **enhancer(function)**: the store enhancer, third party capabilities such as middleware, time travel, persistence, etc. Only applyMiddleware(), ships with Redux
- Do not create more than one store in an application, instead use **combineReducer** to create a root reducer and multiple reducers within that(UI, Entities, Errors, Session)
- 