# nesting

## Nesting and Importing Components

To register a component globally, we first import it in main.js

`import Ninjas from './Ninjas.vue'`

then we pass it as a component for Vue

`Vue.component('ninjas', Ninjas);`

and we pass it as a custom tag inside the template

`<ninjas></ninjas>`

To register a component localy, we import it in the file

`import Ninjas from './Ninjas.vue'`

Then, after we export the default vue instance, we nest it

```js
components: {
    'ninjas': Ninjas
}
```
