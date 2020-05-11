# dynamic_components

They are used when we want to choose which component to output to the browser in a particular place in our template.
First we create the `<component></component>` tag with the is attribute

```md
<component is="component"></component>
```

If we pair it with a dynamic data, we can dynamicaly show different components.

```html
<button @click="component = 'form-one'">Show form one</button>
<button @click="component = 'form-two'">Show form two</button>
```

```js
data () {
  return {
    component: 'form-one'
  }
},
```

The `<keep-alive>` tag allows us to keep the data inside the components, even if we switch between them.

```md
<keep-alive>
  <component :is="component"></component>
</keep-alive>
```
