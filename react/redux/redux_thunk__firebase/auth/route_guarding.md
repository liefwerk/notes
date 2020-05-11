# Route Garding

What if we want to keep users that do not have any account from viewing certain parts of the website ?
We can set up some rules by mapping the state to the props of the component to get the auth prop:

```js
const mapStateToProps = (state) => {
    return {
        auth: state.firebase.auth
    }
}
```

We then pass that `mapStateToProps()` function into the connect HOC

`export default connect(mapStateToProps, mapDispatchToProps)(CreateProject)`

And finally we acces the props and add an if statement to check if we are logged in

```js
const { auth } = this.props
if (!auth.uid) return <Redirect to='/signin' />
```
