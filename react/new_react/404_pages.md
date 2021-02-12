# 404 pages

Let's create a 404 component to show when the user is being adventurous.

We first create a `NotFound` component. It includes a `<Link>` tag that redirects the user to the homepage.

```javascript
import { Link } from "react-router-dom"

const NotFound = () => {
  return (
    <div className="not-found">
      <h2>Sorry</h2>
      <p>That page cannot be found</p>
      <Link to="/">Back to the homepage</Link>
    </div>
  );
}

export default NotFound;
```

We then go to our main `App.js` ad add the new `<Route>`. To get all possibilities we can pass `*` as the path. Remember that we need to put it at the end of the `<Switch>` otherwise it will show this component instead of the other ones.

```javascript
<Route>
    <NotFound path="*" />
</Route>
```