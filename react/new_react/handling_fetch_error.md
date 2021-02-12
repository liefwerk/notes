# Handling fetch error

In case our server has some issue, our we have client-side errors, we can add a `catch()` function in our `fetch()`.

```javascript
fetch('http://localhost:8000/blogs')
    .then(res=> {
        if (!res.ok){
            throw Error('could not fetch the data for that ressource.');
        }
        return res.json();
    })
    .then(data=> {
        setBlogs(data);
        setIsPending(false);
    })
    .catch(err=> {
        console.log(err.message);
    })
```

Now that we can get the error and show it in the console, let's try to output it to the browser. We first create a new state: `const [error, setError] = useState(null);`. Inside our `catch` function we can now pass the error inside that state! `setError(err.message);`.