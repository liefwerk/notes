# Connecting Redux to Firebase

Let's install the packages to interact with the database (API) and sync up the react database with the store.

`npm i react-redux-firebase redux-firestore`

Then we `import` the packages in index.js

```
import firebase from 'firebase/app'
import firebaseConfig from './config/fbConfig'
import { reduxFirestore, getFirestore, createFirestoreInstance } from 'redux-firestore'
import { ReactReduxFirebaseProvider, getFirebase } from 'react-redux-firebase'
```


To link them with thunk, we use the `withExtraArgument()` function

```
const store = createStore(rootReducer, applyMiddleware(thunk.withExtraArgument({getFirebase, getFirestore})));
```

Inside projectActions.js, where we dispatch our action and connect with Firestore, we'll add this new argument

```
export const createProject = (project) => {

    return (dispatch, getState, {getFirebase, getFirestore}) => {// make async call to database
    dispatch({ type: 'CREATE_PROJECT', project })
    }

}
```

But only that won't tell Firebase the project infos and datas. We'll have to use store enhancers.
We already used one in the past, the `applyMiddleware()` function is a store enhancer.
It is possible to combine several store enhancers together.

First, we import `compose` from `redux`

```
import { createStore, applyMiddleware, compose } from 'redux'
```

And inside the store constant, we'll add the compose function to include both of these functions

```
const store = createStore(rootReducer,

    compose(
        applyMiddleware(thunk.withExtraArgument({ getFirebase, getFirestore })),
        reduxFirestore(firebase, firebaseConfig)
    )

);
```

Then we wrap the `App` tag with `<ReactReduxFirebaseProvider>`

```
<ReactReduxFirebaseProvider {...rrfProps}>
    <App />
</ReactReduxFirebaseProvider>
```

And we create a const with all the parameters to pass inside that tag

```
const rrfProps = {

    firebase,
    config: firebaseConfig,
    dispatch: store.dispatch,
    createFirestoreInstance

};
```