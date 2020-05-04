# Route Parameters

There are parts of a URL that can change. Data they show change based on this URL.
Could be a name, an id or else. All showing the same components but different data.

In App.js we create a route for the component that will show the post.

`<Route path="/:post_id" component = {Post} />`

Then we create Post.js, inside we create an id and pass it as a variable.

```
import React, { Component } from 'react'

class Post extends Component {

    state = {
        id: null
    }
    componentDidMount(){
        let id = this.props.match.params.post_id;
        this.setState({
            id: id
        })
    }
    render(){
        return(
            <div className="container">
                <h4>{this.state.id}</h4>
            </div>
        )
    }

}

export default Post
```

## Links

To create a link from the homepage to the individual card, we load the link function

`import {Link} from 'react-router-dom'`

Then wrap the JSX

`Link to={'/'+post.id}><span className="card-title">{post.title}</span><p>{post.body}</p></Link>`

In the Post.js component, we create a state with the post

`state={post:null}`

Then in `componentDidMount()`

```
componentDidMount(){

    let id = this.props.match.params.post_id;
    axios.get('https://jsonplaceholder.typicode.com/posts/' + id, { crossdomain: true })
        .then(res => {
            this.setState({
            post: res.data
        })
    })

}
```

We then use a turnary operator in the render method to check if there are posts or not.
If there are post, we print them.

```
const post = this.state.post ? (

    <div className="post">
        <h4 className="center">{this.state.post.title}</h4>
        <p>{this.state.post.body}</p>
    </div>
    ) : (
        <div className="center">Loading posts...</div>
    )
    
    return(
        <div className="container">
            <h4>{ post }</h4>
        </div>

)
```
