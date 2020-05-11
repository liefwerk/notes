# Setting up Auth

## Setting up Auth with Firebase Auth

When we signin a user in Firebase, it needs a few info as part of the authentification service

```js
email
UID
photo URL
display Name
```

Inside the authentification tab in Firebase, we create a new method of auth (email & password for example).
Then we create a dummy user to test.

To connect firebase to our app we `import` it into the rootReducer.js file

```js
import { firebaseReducer } from 'react-redux-firebase'
```

We then combine it inside the `rootReducer` constant

```js
const rootReducer = combineReducers({
    auth: authReducer,
    project: projectReducer,
    firestore: firestoreReducer,
    firebase: firebaseReducer
})
```

Because authentification has to do with our component Navbar.js, we'll load the state with the mapStateToProps method into this component

```js
// we import connect from react-redux
import { connect } from 'react-redux'

const mapStateToProps = (state) => {
    console.log(state);
    return {// return the right data from the state
    }
}

// we wrap the component with that connect method
export default connect(mapStateToProps)(Navbar)
```
