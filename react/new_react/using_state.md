# Using State

Let's talk about State and Datas. State means the datas we currently use in our component. We already created variable, but if we want to change them we need to create a state.

First of all, let's use a simple way to change a value, with a custom function that attributes a new value to our variable:

```javascript
let name = 'Yoshi';
const handleClick= () => {
    name='luigi';
    console.log(name);
}
```

… and we'll return the value with a `p` tag: `<p>{name}</p>`

This doesn't work because the value isn't reactive. It isn't detected by React. We'll use a `Hook` `useState()`. To use it we first need to import the function from react, then we'll declare a variable with that function.

```javascript
import {useState} from 'react';

const [name, setName] = useState('mario');
```

```javascript
const handleClick= () => {
    setName('luigi');
}
```

Now if we call the function `handleClick` it will change the value.