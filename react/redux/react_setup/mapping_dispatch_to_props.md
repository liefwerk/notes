# Maping States to Props

We might want to map states to props when we want to interact/delete the props.
Here's a recap of what happends when we want to make a change to a prop:

**1- To make a change, we have to dispatch an action from the component.**
That action will contain a type and an optional payload.
In the case of deleting a post, could be the id of the post.

**2- Then, that action is dispatched to the reducer.**
Checks the type, takes the payload and make the change to the central store.

**3- Then we get the updated props inside the component.**
Creating the mapDispatchToProps function

```js
// the function takes the dispatch as a parameter
const mapDispatchToProps = (dispatch) => {

    return {
    // inside the function we return the delePost function (which takes an id as a parameter)
    // and we call the dispatch function which takes an object with a type and an id
        deletePost: (id) => { dispatch({type: 'DELETE_POST', id: id}) }
    }

}
```

We then pass the `mapDispatchToProps()` function inside the `connect()` function

`export default connect(mapStateToProps, mapDispatchToProps)(Post)`

Inside the JSX we create a button that will fire the `deletePost()` function

```js
<div className="center">

    <button className="btn grey" onClick={this.handleClick}>Delete Post</button>

</div>
```

Then we create athat `handleClick()` function

```js
handleClick = () => {

    this.props.deletePost(this.props.post.id)

}
```

We then go to the rootReducer.js file that will handle the next steps.

```js
const rootReducer = (state = initState, action) => {
    // check the type of action
    if (action.type === 'DELETE_POST'){// we'lluse the filter method
        let newPosts = state.posts.filter(post => {
        // when the action.id is not post.id it will return true, when it is equal it will return false and filter it.
        return action.id !== post.id
        })// and we return the new state
        return {// let's not forget to add the other props of the state with the spread operator
            ...state,
            posts: newPosts
        }
    }
    return state;
}
```
