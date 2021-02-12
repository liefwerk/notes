# Fetching data with useEffect

We'll fetch the data once the component renders. Let's first empty all the state an set the initial value of blogs to null.

```javascript
useEffect(() => {

    fetch('http://localhost:8000/blogs')
     .then(res=> {
        return res.json();
     })
     .then(data=> {
        console.log(data);
        setBlogs(data);
     })
    }, []);
```

Let's then edit our JSX template by adding some react conditions so we'll only show the `Blogs` component when it has been successfully fetched.

```javascript
return (
    <divclassName="home">
        <h2>Homepage</h2>
        {blogs && <BlogList blogs={blogs} title="All Blogs!" handleDelete={handleDelete}/>}
    </div>
);
```

