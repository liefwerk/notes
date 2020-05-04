# Links, Navlinks and Redirect

In Navbar.js,

`import {Link,NavLink} from 'react-router-dom'`

## Link

Changes the anchor tags `<a>` with `<Link to=""> </Link>`
That prevents the page from reloading when you click them.

## NavLink

It adds the class active to the elements in the navbar.
Simply replace `<Link>` by `<NavLink>.`

## Programmatic Redirect

Router information is also included in the props object.

We can do a redirection using the props method `push()`

`props.history.push('/about')`

We have to put it before the return.

## Higher Order Component

Wraps another component and gives it extra powers.

If we want to get the router props of an element that isn't in the Routing, we have to use a Higher Order Component.
In the example of Router, it is the Component `withRouter()`.
Then the HOC wrappes the Component in the export function

`export default withRouter(Navbar)`

Here's a custom one created for the example:

```
import React from 'react'

const Rainbow = (WrappedComponent) => {

    const colours = [
        'red',
        'pink',
        'orange',
        'blue',
        'green',
        'yellow'
    ]
    
    const randomColour = colours[Math.floor(Math.random() 5)]
    const className = randomColour + '-text'
    
    return (props) => {
        return (
            <div className = {className}>
                <WrappedComponent {...props}/>
            </div>
        )
    }

}

export default Rainbow
```

When we return, we include the props and inside the tag `WrappedComponent` the spread the props like this:

```

{...props}
```

then `export default` the component.