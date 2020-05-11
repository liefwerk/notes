# input_binding

Nothing really new, we already saw this with the `v-model` attribute.

A good modifier to add though is .lazy, that will output the data only when we change the field or click outside of it.
We can also organise our data in the form of objects:

```html
<p>Blog title:</p>
<h1>{{blog.title}}</h1>
<p>Blog content:</p>
<p>{{blog.content}}</p>
```

```js
data() {
    return {
        blog: {
            title: "",
            content: ""
        }
    }
}
```
