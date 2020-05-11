# Redux Actions

```js
// we create a new action and we describe it in the type
// const action = {type, payload}
const todoAction = {type: 'ADD\_TODO', todo: 'buy milk'}
```

To dispatch an action:

`store.dispatch(todoAction);`
