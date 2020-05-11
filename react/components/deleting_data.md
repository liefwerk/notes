# Deleting Data

We construct a new function `deleteNinja()`, in this function we'll take the id of the props and apply the `filter()` method.

```js
deleteNinja = (id) => {

* let ninjas = this.state.ninjas.filter(ninja => {
* * return ninja.id !== id
* })
* this.setState({
* * ninjas: ninjas
* })

}
```

It is important to use `setState()` to apply the change, otherwise it modifies directly the array.

In Ninja.js, we add a button with an onClick attribute to trigger the `deleteNinja()` function.

```js
<button onClick = {() => { deleteNinja(ninja.id) }}>DeleteNinja</button>
```

That function is passed inside an anonymous function so it isn't triggered when it is first loaded in the DOM.
