# Click events and functions

When we have a website, there are loads of different events. In this chapter we'll look at the click event.

## Linking a function

Let's create a button: `<button>Click me!</button>`.

We also create a new function:

```javascript
const handleClick = () => {
    console.log('hello ninjas');
}
```

We can link that function to the button this way: `<button onClick={handleClick}>Click me!</button>`.

### Passing an argument

If we do the same thing with an argument, it would call the function over and over again.
So, to pass an argument we need to wrap it inside an anonymous function: 
```javascript
<button onClick={() => handleClickAgain('Luigi')}>Click me again!</button>`
```

… and our new function:

```javascript
const handleClickAgain= (name) => {
    console.log('Goodbye '+name);
}
```

## The Even parameter

Taking the first function, we can pass an event parameter `e`:

```javascript
const handleClick = (e) => {
    console.log('hello ninjas',e);
}
```

Taking the second function we can write this to apss the event parameter:

```javascript
<button onClick={(e) => handleClickAgain('Luigi', e)}>Click me again!</button>`
```

… and our second function:

```javascript
const handleClickAgain= (name, e) => {
    console.log('Goodbye '+name, e.target);
}
```