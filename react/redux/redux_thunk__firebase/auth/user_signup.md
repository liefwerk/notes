# User Signup

First, let's create the action:

```js
export const signUp = (newUser) => {
    return (dispatch, getState, {getFirebase, getFirestore}) => {
        const firebase = getFirebase();
        const firestore = getFirestore();
        firebase.auth().createUserWithEmailAndPassword(
            newUser.email,
            newUser.password
            ).then(resp => {
                return firestore.collection('users').doc(resp.user.uid).set({
                    firstName: newUser.firstName,
                    lastName: newUser.lastName,
                    initials: newUser.firstName[0] + newUser.lastName[0]
                })
            }).then(() => {
                dispatch({ type: 'SIGNUP_SUCCESS' });
            }).catch((err) => {
                dispatch({ type: 'SIGNUP_ERROR', err});
            }
        )
    }
}
```

We then handle it inside our Reducer

```js
case 'SIGNUP_ERROR':
console.log('signup error');
    return {
    ...state,
    authError: action.err.message
}

case 'SIGNUP_SUCCESS':
    return {
    ...state,
    authError: null
}
```

Then in the SignUp.js component we add the dispatch to props

```js
const mapDispatchToProps = (dispatch) => {
    return {
        signUp: (newUser) => dispatch(signUp(newUser))
    }
}
```

and we pass the state in the function in the `handleSubmit()` function

```js
handleSumbit = (e) => {

e.preventDefault();
this.props.signUp(this.state)

}
```
