# register_locally

What if we have filters or directives that we only use in one component ?
We register them locally.

```js
filters: {
    toUppercase(value){
        return value.toUpperCase()
    }
}
```
