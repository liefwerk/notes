# Route parameters

Sometime we need to pass dynamic values in parts of the route. An example is for a blog's detail page: `/blogs/123`. That `123` could be any number. We show a single component but with different content.

Let's first create a `BlogDetails.js` component.

```javascript
import { useParams } from "react-router-dom";

const BlogDetails = () => {

  const { id } = useParams();

  return (
    <div className="blog-details">
      <h2>Blog details - {id}</h2>
    </div>
  );
}

export default BlogDetails;
```
We then change our `<Route>` parameter to include the id in the params:

```javascript
<Route path="/blogs/:id">
    <BlogDetails />
</Route>
```

Finally we add this route to the blog list in the component named `BlogList`:

```javascript
<div className="blog-preview" key={blog.id}>
    <Link to={`/blogs/${blog.id}`}>
        ...
    </Link>
</div>
```