# Initial Setup

First we install the packages required to start coding

`npm i redux react-redux`

Then we import the library into the index.js file

```js
import { createStore } from 'redux'
import { Provider } from 'react-redux'
```

We create the store with that function, and inside we'll pass the reducer (function that handles the changes)

`const store = createStore(rootReducer);`

To activate the store, we wrap the `<App />` tag with `<Provider store={store}></Provider>.`

Then, we create the reducer in another file that we can call rootReducer. It is recommended to have differents reducers for different tasks.

```js
const initState = {
    posts: []
}

const rootReducer = (state = initState, action) => {
    return state;
}

export default rootReducer
```
