# Outputting lists

For our blog, we'll create a new array of objects called `blogs`.

```javascript
const [blogs, setBlogs] =useState([

    { title: 'My new website', body: 'lorem ipsum...', author: 'mario', id: 1 },
    { title: 'Welcome party!', body: 'lorem ipsum...', author: 'yoshi', id: 2 },
    { title: 'Web dev top tips', body: 'lorem ipsum...', author: 'mario', id: 3 }

]);
```

To return our list we'll have to cycle through the array and output a template for each one. We'll use the `map` method: `blogs.map(() => ())`

```javascript
{blogs.map((blog)=> (
    <div className="blog-preview" key={blog.id}>
        <h2>{blog.title}</h2>
        <p>Written by {blog.author}.</p>
    </div>
))}
```