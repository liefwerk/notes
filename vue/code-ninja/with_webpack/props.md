# props

Very similar to Props in React
With props we can pass data from a parent component to a child component.

First, we lay the ground to receive the props in the component file

```js
export default {
    props: ['ninjas'],
        data() {
            return {
        }
    }
}
```

Then in the parent file we pass it inside the custom tag

```js
// it is important to put v-bind or : before the property to make it dynamic
<ninjas :ninjas="ninjas"></ninjas>
```

We can also use validation in the receiving end to be sure to receive the right kind of data

```js
props: {
    ninjas: {
        type: Array,
        required: true
    }
}
```
