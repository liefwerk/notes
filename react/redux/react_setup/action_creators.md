# Action Creators

To make an action more reusable, we can use action creators to create them inside another file.

When we call that function, it will generate an action an return it.
If we cant to dispatch the same action in a few components it gets easier.

First let's create a new folder actions in which we'll place a new file called postActions.js. Inside that file we'll create an action called `deletePost()`

```
export const deletePost = (id) => {

    return {
        type: 'DELETE_POST',
        id
    }

}
```

We import that new function in the Post.js file:

```
import { deletePost } from '../actions/postActions'
```

Then we can edit our mapDispatchToProps() function to include that new action

```
const mapDispatchToProps = (dispatch) => {

    return{
        deletePost: (id) => { dispatch(deletePost(id)) }
    }

}
```
