# useEffect Hook

We've seen one hook called `useState()`. Another hook is called `useEffect` - it is loaded every time the DOM is rendered.

## How to use it ?

To use it we have to import it: `import { useState, useEffect } from'react';`. Then we can put it before our return statement:

```javascript
useEffect(() => {
    console.log('use effect ran');
});
```

We can also access the `state` inside `useEffect`.

```javascript
useEffect(() => {
    console.log('use effect ran');
    console.log(blogs);
});
```

Updating the `state` inside the `useEffect` function can cause an infinite loop because it is called every time the state is changed. We'll see later on how to prevent it.

## useEffect dependencies

The useEffect hook can have our custom functions, but sometimes we don't want to fire that function at every render. A way to achieve this is to add a dependency array to the `useEffect` function.

```javascript
useEffect(() => {
    console.log('use effect ran');
    console.log(blogs);
}, []);
```

This way, it won't run the function at every render.

Now, what if we want to run `useEffect` only on a particular `state` change ?

```javascript
const [name, setName] = useState('mario');

useEffect(() => {
    console.log('use effect ran');
    console.log(blogs);
}, [name]);

<button onClick={() => setName('luigi')}>change name</button>
```