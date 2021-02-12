# Submit events

For submitting a form we have two choices: either fire a function linked to the button or make a submit event. In our case we'll make a submit event.

```javascript
const handleSubmit = (e) => {
    e.preventDefault();
    const blog = { title, body, author };
}

<form onSubmit={handleSubmit} >
```