# Axios

To request data from an external server, we can install an external package called `Axios`

`npm install @nuxtjs/axios`

First, if needed we convert the function into a class and insert the method `ComponentDidMount()`
Inside, we call the get function from axios:

```
axios.get('https://jsonplaceholder.typicode.com/posts', { crossdomain: true })

.then(res => {
console.log(res);
this.setState({
posts: res.data.slice(0, 10)
})

})
```


`crossdomain: true` is useful when it isn't from the same domain, otherwise it might throw an error.

Then after the render, we create an array with all these posts (with the turnary operator to handle when they are no posts.)

```
const { posts } = this.state
const postList = posts.length ? (

    posts.map(post => {
        return (
            <div className="post card" key={post.id}>
                <div className="card-content">
                    <span className="card-title">{post.title}</span>
                    <p>{post.body}</p>
                </div>
            </div>
        )
    }) : (
    <div className="center">No posts yet.</div>
    
)
```
