# Controlled inputs

Let's put our attention to web form so we can add a blog post to the data. Controlled inputs are a way to setup inputs and track the value. We'll keep the value in a state and when it changes the value is also changed. It will be in sync.

Let's open the `Create` component and add a form.

```javascript
const Create = () => {

  const [title, setTitle] = useState('');
  const [body, setBody] = useState('');
  const [author, setAuthor] = useState('yoshi');

  return (
    <div className="create">
      <h2>Add a New Blog</h2>
      <form>
        <label>Blog title:</label>
        <input
          type="text"
          required
          value={title}
          onChange={(e) => setTitle(e.target.value)}
        />
        <label>Blog body:</label>
        <textarea
          required
          value={body}
          onChange={(e) => setBody(e.target.value)}
        />
        <label>Blog author:</label>
        <select
          value={author}
          onChange={(e) => setAuthor(e.target.value)}
        >
          <option value="mario">mario</option>
          <option value="yoshi">yoshi</option>
        </select>
        <button>Add blog</button>
        <p>{title}</p>
        <p>{body}</p>
        <p>{author}</p>
      </form>
    </div>
  );
}
```

We first create our `form` with two `input` and one `select`. Inside we set the value as `title` from the state and we add an `onChange` attribute to fire a function called `setTitle` also from the state.

This process is the same for all inputs.

```javascript
<label>Blog title:</label>
<input
    type="text"
    required
    value={title}
    onChange={(e) => setTitle(e.target.value)}
/>
```