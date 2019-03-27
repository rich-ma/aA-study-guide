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
// takes 3 arguments, but two optional, requires a reducer
store.subscribe(() => {
  document.body.innerText = store.getState();
})

document.addEventListener('click', () => {
  store.dispatch({ type: 'INCREMENT' })
})
// this version has an issue because it never displays the initial state of the store(0);
//to fix this, we create a new function called render put the subscribe logic into it, and call it whenever the state changes, triggering the subscribe function

const render = () => {
  document.body.innerHTML = store.getState();
}

store.subscribe(render);
render(); //initial call to display initial state;

document.addEventListener('click', () => {
  store.dispatch({ type: 'INCREMENT' })
})
```
- createStore takes 3 arguments, createStore(reducer, preloadedState, enhancer)
  - **reducer(function)**: a reducing function that returns the next state tree, given the current state tree and an action to handle
  - **preloaded state**: the initial state, can hydrate the state from the server in a universal app, or restore prev. serialzed user session/
    - if you use combineReducers, you need to give a preloaded state with the same shape as the keys passed to it.
  - **enhancer(function)**: the store enhancer, third party capabilities such as middleware, time travel, persistence, etc. Only applyMiddleware(), ships with Redux
- Do not create more than one store in an application, instead use **combineReducer** to create a root reducer and multiple reducers within that(UI, Entities, Errors, Session)

## 7. Implementing Store from Scratch
- need to keep track of our subscriptions, so we create an array of listeners, everytime subscribe is called we push a new listener into the array.
- we need to dispatch actions as well, the state update with the reducer and the new action, then each listener is updated 
- to unsubscribe we filter out the current listener using a function that filters it from the filter array.
- when the store is returned, we want the initial state to be populated.

## 8. React Counter Example


## 9. Avoiding array mutation with concat(), slice(), and ...spread
- to ensure that we are not modifying the original state, we use these methods to protect it.
- also use deepFreeze() to lock the state from being mutated.
- this allows us to test our code fluidly.
- For example. say we have an array of numbers representing counters
- if we wanted to add a counter, we can't just push a new counter onto the list, as that would mutate the existing array
  - instead we can return a spread of the original list and the new counter "return [...list, 0]
- If we wanted to remove a counter from the list, we can't use splice() because that mutates as well
  - instead, we slice from 0 to the index, and from the index+1 to the end.
  - "return list.slice(0, index).concat(list.slice(index+1))"
  - cleaner way "return [...list.slice(0, index), ...list.slice(index+1)]
- if we wanted to increment an index we cant just index into the list "list[index]++" becuase that mutates as well.
  - instead, we return a new object using slice
  - return [...list.slice(0, index), list[index] + 1, ...list.slice(index+1)];
  - 

## Creating a reducer
- we use deepfreeze to prevent accidental writing on state
- reducer: pure function to implement update logic of application, how next state is calculated given current state and action.
- write a test with first state, action, and expected state.
- reducer takes two arguments, state, and action.
- reducer uses a switch statement to look at the action type to see if it matches any of the cases the reducer is in charge of
- will create a new object and add it to the state with an object using all the info from the action (id, text, and completion)

ex. 
```javascript
const todos = (state = [], action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return [
        ...state,
        {
          id: action.id,
          text: action.text,
          completed: false
        }
      ];
    default:
      return state;
  }
};

const testAddTodo = () => {
  const stateBefore = [];
  const action = {
      type: 'ADD_TODO',
      id: 0,
      text: 'Learn Redux'
  };
  const stateAfter = [{
      id: 0,
      text: 'Learn Redux',
      completed: false
  }];

  deepFreeze(stateBefore);
  deepFreeze(action);

  expect(
    todos(stateBefore, action)
  ).toEqual(stateAfter);
};

testAddTodo();
console.log('All tests passed')
```
- we create a todoReducer here that is able to add todo, and toggle todo.
- toggle looks for a todo with matching id, and flips its 'completed' state.

## reducer composition with Arrays
- 