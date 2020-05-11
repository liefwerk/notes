# Logging Out

## Creation of the Logging Out Component

Firstly, we add an action

```js
export const signOut = () => {
    return (dispatch, getState) => {
        firebase.auth().signOut().then(() => {
            dispatch({type: 'SIGNOUT_SUCCESS'})
        })
    }
}
```

Then we write the cases in the switch method of the authReducer.js file

```js
switch {
case 'SIGNOUT_ERROR':
    console.log('signout error');
    return {
        ...state,
        authError: 'Logout failed'
    }
case 'SIGNOUT_SUCCESS':
    console.log('signout success');
    return {
        ...state,
    authError: null

    }
}
```

We then connect it as an HOC to the right component, `mapDispatchToProps`, import the props and pass that function (that is inside the props)

```js
// let's not forget to pass the props
const SignedInLinks = (props) => {

// and here we pass the function in the onClick attribute of the Sign Out link
<a onClick={props.signOut}>Log Out</a>
```
