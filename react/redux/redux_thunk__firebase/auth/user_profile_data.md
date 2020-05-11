# User Profile Data

The user data store in firestore isn't always synced in in our state, we have to manually sync it in to use it in our component.
Firstly in index.js we pass a constant with a few configs to access that profile from firestore

```js
const profileSpecificProps = {
    userProfile: 'users',
    useFirestoreForProfile: true,
    enableRedirectHandling: false,
    resetBeforeLogin: false
}
```

We then pass the const inside the config

```js
const rrfProps = {
    firebase,
    config: profileSpecificProps,
    dispatch: store.dispatch,
    createFirestoreInstance,
}
```

Inside Navbar.js we pass it inside the props objects

```js
const mapStateToProps = (state) => {
    return {
    auth: state.firebase.auth,
     profile: state.firebase.profile
    }
}
```

And load in into the `<SignedInLinks>` component as a prop

```js
const { auth, profile } = props
const links = auth.uid ? <SignedInLinks profile={profile} /> : <SignedOutLinks />
```

Inside that component, we use the prop to show the initials

`<li><NavLink to='/' className="btn btn-floating pink lighten-1">{props.profile.initials}</NavLink></li>`
