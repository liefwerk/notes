# Redux Reducers

Reducers are used to interact with the data center.

```
// we create the reducer as a function that will pass the state and the action
function myreducer(state = initState, action){
    if (action.type == 'ADD\_TODO'){// we return the new state and edit it
        return {// we create a new array to edit in a non-destructive waystate,
            todos: \[...state.todos, action.todo\]
        }
    }
}
```

## Root Reducer

If we have a few reducers, it is good practice to dedicate a single file to each of them and then merge them inside a rootReducer.js file.
Here's an excerpt from a standart rootReducer.js file:

```
// we import the other reducers
import authReducer from './authReducer'
import projectReducer from './projectReducer'
// we import the combineReducer method
import{ combineReducers } from 'redux'

// we create the rootReducer
const rootReducer = combineReducers({

auth: authReducer,
project: projectReducer

})

// we export it
export default rootReducer
```

We then import it to the index.js file

```
import rootReducer from '/store/reducers/rootReducer'
```

and pass it inside the `createStore()` method

`const store = createStore(rootReducer);`