# Reusing components

## Filter function

Let's add a new `Blog` Component in our `Home` Component:

```javascript
<BlogList blogs={blogs} title="All Blogs!"/>
<BlogList blogs={blogs.filter((blog) => blog.author === 'mario' )} title="Mario's blogs"/>
```

The `filter` function now filters our list without deleting it.

But how can we do if we want to delete an item ?

## Functions as props

We'll nee a button for each blog post: `<button onClick={() => handleDelete(blog.id)}>delete blog</button>`. We then create the function `handleDelete` inside the component that has the blogs:

```javascript
const handleDelete= (id) => {
    const newBlogs= blogs.filter(blog=> blog.id!==id);
    setBlogs(newBlogs);
}
```

… and pass the function to our `BlogList` component:

```javascript
<BlogList blogs={blogs} title="All Blogs!" handleDelete={handleDelete}/>
```

Let's not forget to pass the function `handleDelete` as a prop in the `BlogList` component:

`constBlogList= ({ blogs, title, handleDelete }) => { ... }`

That is how we can pass `functions` between `components` as `props`.