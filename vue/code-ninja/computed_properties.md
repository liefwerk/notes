# computed_properties

The issue with the instances and its methods is that each time a method is called, it will also call the other ones.
Here's a way to call only when a value is changed.

We can use the computed object this way

```js
computed: {
    addToA: function(){
        // console.log('addToA');
        return this.a + (this.age)
    },
    addToB: function(){
        // console.log('addToB');
        return this.b + this.age
    }
}
```

It will only run when needed.
