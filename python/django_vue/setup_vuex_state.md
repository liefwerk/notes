# Setting up the store

Let's go to the `store/index.js` file. This currently has the following structure:

```javascript
import { createStore } from 'vuex'

export default createStore({
  // These are the variables and information
  state: {
  },
  // it is an synchronous mutation to a variable
  mutations: {
  },
  // it is asynchronous function to change the variables
  actions: {
  },
  // i'm not quite sure...
  modules: {
  }
})
```

inside the `state` we'll add a few variables.

```javascript
...
state: {
    cart: {
      items: [],
    },
    isAuthenticated: false,
    token: '',
    isLoading: false
  },
...
```

