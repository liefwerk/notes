# Multiple components

We currently have a single component called `App.js`. it is the first that gets rendered and sits at the top of the application.

If we were to make more component, we nest it inside this root component. This makes up our component tree.

## Making a new component

Let's create `Navbar.js`. To start a new file and a static component let's write `sfc` and then press `Tab`.

This creates this code:

```javascript
const Navbar = () => {

return ( );
}
export default;
```