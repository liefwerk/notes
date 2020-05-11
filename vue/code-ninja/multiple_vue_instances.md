# multiple_vue_instances

Firstly, we put the `new Vue({})` method inside a variable

```js
const one = new Vue({
    el: '#vue-app-one',
    data: {},
    methods: {},
    computed: {}
});
```

There is a possible interaction between them.
The variable names permit a reference outside of their own scope.

For example, in the second app we could create a function to change the first app's title

```js
const one = new Vue({...})

const two = new Vue({...

changeTitle: () => {
one.title = "Title changed"
}

...})
```

It also possible to call that function outside of the methods, straight from the script.js file.
