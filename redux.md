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
- 
