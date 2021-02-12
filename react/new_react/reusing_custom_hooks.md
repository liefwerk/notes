# Reusing custom hooks

Going to a blog detail page, we can use the `id` to `fetch` our API. We just need to use our hook `useFetch`.

```javascript
const BlogDetails = () => {

  const { id } = useParams();
  const { data: blog, error, isPending } = useFetch('http://localhost:8000/blogs/' + id);

  return (
    <div className="blog-details">
      {isPending && <div>Loading...</div>}
      {error && <div>{error}</div>}
      {blog && (
        <article>
          <h2>{blog.title}</h2>
          <p>Written by {blog.author}</p>
          <div>{blog.body}</div>
        </article>
      )}
    </div>
  );
}
```

Our `useFetch` has easily been reused in this case.