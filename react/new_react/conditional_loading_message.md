# Conditional loading message

Let's create a loading message for when our data is being fetched.

We first create a state to follow the state of the fetching: `const [isPending, setIsPending] = useState(true);`. Then we add some conditions to our JSX below: `{isPending && <div>Loading...</div>}`.

To finish, we need to add the state `isPending` to false with the function `setIsPending`. We'll put it just after we fetch the data:

```javascript
...
    .then(data=> {
        console.log(data);
        setBlogs(data);
        setIsPending(false);
    })
...
```