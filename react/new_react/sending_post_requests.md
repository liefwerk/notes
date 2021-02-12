# Sending POST requests

Next step is to create a `POST` request. We'll make it inside our handleSubmit function because we won't be doing other POST requests in this application.

We'll start by adding a `fetch` function in our `handleSubmit` function.

```javascript
fetch('http://localhost:8000/blogs', {
    method: 'POST',
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(blog)
}).then(() => {
    console.log('new blog added');
})
```

We can then add a `isPending` state to change the appearance of our button and make it disabled when it is fetching the data.

```javascript
const [isPending, setIsPending] = useState(false);

{!isPending && <button>Add blog</button>}
{isPending && <button disabled>Adding blog...</button>}
```