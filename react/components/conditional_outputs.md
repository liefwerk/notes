# Conditional Outputs

## Conditions and turnary operator

### The turnary operator

`// condition ? (if true) : (if false)`

The condition is stated as follows:

```js
return ninja.age > 20

then

?
```

then the JSX inside the first if true, etc..

```js
return ninja.age > 20 ? (

<div className="ninja" key={ninja.id}>
    <div>Name: {ninja.name}</div>
    <div>Age: {ninja.age}</div>
    <div>Belt: {ninja.belt}</div>
</div>

) : (null);
```
