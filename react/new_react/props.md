# Props

In our `Home` component we are outputting a list of blogs. In real life, we might need this list in several pages. Instead of repeating the same code, we can make transform this piece of code into a `Component`.

Let's create a `BlogList` component. To pass data inside these components we'll use `props`.

```javascript
const BlogList = (props) => {

    const blogs = props.blogs;
    
    return (
        <div className="blog-list">
            {blogs.map((blog) => (
            <div className="blog-preview"key={blog.id}>
                <h2>{blog.title}</h2>
            <p>Written by {blog.author}.</p>
            </div>
            ))}
        </div>
    );
}

export default BlogList;
```

We'll also have to pass the props inside our component declaration in the `Home` component: `<BlogListblogs={blogs}/>`.

Props can be a string or a dynamic value.