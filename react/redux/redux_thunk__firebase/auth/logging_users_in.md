# Logging Users In

Firstly, to handle the action we have to create an action creator with the file authActions.js

```
import firebase from 'firebase/app'
import 'firebase/auth';

export const signIn = (credentials) => {
    return (dispatch, getState) => {
        const firebase = getFirebase();
        
        firebase.auth().signInWithEmailAndPassword(
            credentials.email,
            credentials.password
        ).then(() => {
            dispatch({type: 'LOGIN_SUCCESS'})
        }).catch((err) => {
            dispatch({type: 'LOGIN_ERROR', err})
        })
    }
}
```

Then, once that action is dispatched it will reach our authReducer.js file, we have to handle these few cases

```
const authReducer = (state = initState, action) => {
    switch(action.type){
    case 'LOGIN_ERROR':
        console.log('login error');
        return {
            ...state,
            authError: 'Login failed'
        }
    case 'LOGIN_SUCCESS':
        console.log('login success');
        return {
            ...state,
            authError: null
        }
        default:
            return state;
    }
}
```

The reducer updates the state, now it is time to map the state to the props of the SignIn Component

```
const mapStateToProps = (state) => {
    return {
        authError: state.auth.authError
    }
}
```

Let's not forget to pass it as an HOC

```
export default connect(mapStateToProps, mapDispatchToProps)(SignIn)
```

We can optionally pass that error inside the JSX and output it in the HTML login page

```
<div className="red-text center">

{ authError ? <p>{authError}</p> : null}

</div>
```