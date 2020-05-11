# intro_to_components

## Components in Vue.js

First we create the compoent in a .js file

```js
Vue.component('greeting', {
    template: '<p>Hey there, i\'m a reusable component</p>'
});
```

Then in the HTML we create the custom tag

`<greeting></greeting>`

To interact with data inside a component, we have to pass it as a function first, otherwise each instance if the component will be change once one is alterated.

```js
Vue.component('greeting', {

template: '<p>Hey there, i\'m {{ name }}</p>',
    data: () => {
        return {
            name: Yoshi;
        }
    }
});
```
