# conditionals

## (v-if & v-show)

To express conditionals, we can use `v-if` and `v-show`.

```html
// there we add a click event to change the boolean values
<button @click="error = !error">Toggle Error</button>
<button @click="success = !success">Toggle Message</button>

// and we add an if statement that shows the p tag only when it's respective boolean value is true
<p v-if="error">There has been an error, dang!</p>

// v-else-if is similar to the else statement in JS
<p v-else-if="success">Whoo, succes :)!</p>
```

```js
data: {
    success: false,
    error: false
}
```

The difference between `v-show` and `v-if` is that `v-show` doesn't take the element out of the DOM, it puts the display as none.
