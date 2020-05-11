# Store Subscriptions

Here is the basic idea - listen to changes in the store the react to it.

```js
store.subscribe(() => {
    // function fires everytime there is a change
    console.log('state updated');// to access the state we do store.getState()
    console.log('store.getState()');
})
```

The problem is that the state (object with todos and posts) get overridden by the new one.
We also pass the data that we don't want to change.

In the myreducer function, we pass the full state as a spread operator

```js
// we create the reducer as a function that will pass the state and the action
function myreducer(state = initState, action){

    // if action type is add todo
    if (action.type == 'ADD_TODO'){// we return the new state and edit it
        return {// we create a new array to edit in a non-destructive way
            ...state,todos: [...state.todos, action.todo]
        }
    }
    // if action type is add post
    if (action.type == 'ADD_TODO'){
        // we return the new state and edit it
        return {
            // we create a new array to edit in a non-destructive way
            ...state,
            posts: [...state.posts, action.posts]
        }
    }
}
```

To keep on going with the examples, here's a couple of actions:

```js
store.dispatch({type: 'ADD_TODO', todo: 'buy milk'});
store.dispatch({type: 'ADD_TODO', todo: 'sleep some more'});
store.dispatch({type: 'ADD_TODO', post: 'Egg hunt with yoshi'});
```
