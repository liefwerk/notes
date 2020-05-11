# Redux Stores

A central data store is a js object that represents the global state of our application.
The reducer interacts with the central data store. State is always updated from this one single place.

When we create a store, we pass a single recuder function. Then store knows wich one to follow.

Here's an example with code snippets.

```js
// we load the function createStore
const { createStore } = Redux;

//we initiate the state
const initState = {

todos: [],
posts: []

}

// we create the reducer as a function that will pass the state and the action
function myreducer(state = initState, action){

}

// we create the store
const store = createStore(myreducer)
```
