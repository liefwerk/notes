# Maping States to Props

First, we import the connect function inside the Component we want to change

`import { connect } from 'react-redux'`

Then we invoke it as a Higher Order Component when exporting the Component and we pass a map function inside

```
// connect(mapfunction(Component))
export default connect(mapStateToProps)(Home)
```

This means that our Component can now connect itself to Redux.
Here's the function that we pass inside the connect function

```
// it takes the state of the component and returns it in an object
const mapStateToProps = (state) => {
    return {
        posts: state.posts
    }
}
```

Then inside the `render()` method of the Component, we pass the props like this

`const { posts } = this.props`

When there is an array we need to loop through, the map function is our savior.

```
array.map(item =>{

    return (
        <tag attribute={item} key={item.id} />
    )

}

{ projects && projects.map(project =>{

    return (
        <ProjectSummary project={project} key={project.id} />
    )

})}
```
