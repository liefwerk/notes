# events

## (v-on)

To listen to events, we use the directive `v-on` or `@`

```html
<button v-on:click="add">add a year</button>
<button v-on:click="subtract">subtract a year</button>
```

```js
// and inside the script.js we write the 2 methods
methods: {
    add: function(){
        this.age++;
    },
    subtract: function(){
        this.age--;
    }
}
```

Say we want to react to a double click, we can use `v-ondbclick`, same with mousemove - check [the reference for the other ones.](https://vuejs.org/v2/guide/events.html)

## Event Modifiers

They allow to tackle on advanced scripts.
To attach a modifier we do `@click.modifier="`"

It also works with the keyboard, we just have to add a modifier `.enter`, `.tab` or `.alt`
