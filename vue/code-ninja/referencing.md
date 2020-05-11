# referencing

## with $refs

With Vue gives us a way to reach into the template, grab an element and get data about this element.

```js
<input type="text" ref="input" />
<button @click="readRefs"></button>
```

We can now access this element from the js file.

```js
readRefs: function(){
    this.output = this.$refs.input.value
}
```
