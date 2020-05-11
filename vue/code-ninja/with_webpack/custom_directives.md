# custom_directives

All directives start with v- (like v-for, v-model etc...).
What if we want to do something but the directive doesn't exist ?

We can create our own directive. In this example we'll create one that will trigger a random colour: v-rainbow.
First, we'll head into the main.js file

```js
// custom directives
Vue.directive('rainbow', {

    // here we control it's functionality// bind fires as soon as the component hooks up
    bind(el, binding, vnode){
        el.style.color = "#" + Math.random().toString().slice(2, 8);
    }
})
```

Then let's not forget to hook our directive into a tag.

`<h2 v-rainbow>{{blog.title}}</h2>`

We can also add v-theme:column and access it through binding.arg.
