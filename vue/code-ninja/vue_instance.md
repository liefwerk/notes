# vue_instance

## Vue Instance, Data & Methods

Vuejs works with instance, let's create one

```js
// firstly we create an instance
// it is possible to have a few vue instances, each one will control a certain part of the website
// in this case we'll use only one instance

new Vue({

// targets <div class="" id="vue-app"></div>
el: '#vue-app',
    data: {
        name: 'Nathanaël'
    }
});
```

We can store as much as we want inside an instance, methods for example

```js
new Vue({

// targets <div class="" id="vue-app"></div>
el: '#vue-app',
    data: {
        name: 'Nathanaël',
        job: 'Ninja'
    },
    methods: {
        greet: function(time){
            return 'Good ' + time + ' ' + this.name
    }
}

});
```
