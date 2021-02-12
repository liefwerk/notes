# Deleting blogs

We can successfully list blogs, create one and now we want to be able to delete one.

Over to blog details: `<button onClick={handleClick}>delete</button>`.

We create a function called `handleClick`:

```javascript
const history = useHistory();

const handleClick = (e) => {
    fetch('http://localhost:8000/blogs/' + blog.id, {
        method: 'DELETE'
    }).then(() => {
        history.push('/');
    })
}
```