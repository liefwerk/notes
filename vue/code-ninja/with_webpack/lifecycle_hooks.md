# lifecycle_hooks

When we create a new instance, the first one is `beforeCreate()`
Then the instance observes any data and initializes events.

`created()` lifecycle methods arrived after that. Good place to interact with bus or data.
And also great place to fetch external data.

If we don't have an `el` option, `vm.$mount(el)` is called.
If we do, it checks if there is a template.

When it compiles the tempalte, it's about to mount the DOM.
Before it does mount the DOM we have `beforeMount()`

Once it has mounted the DOM ( `mounted()` ), we have access to the code in the DOM.
To manipulate the DOM we can do it here.

We then have `beforeUpdate()` and `updated()`

If we want to get rrid of the component, we can get ay code before it's destroyed with `beforeDestroy()`
