# looping

## (v-for)

We use `v-for` to loop through an array

```js
// here's the list
characters: ['Mario', 'Luigi', 'Yoshi', 'Bowser']

<div class="ul">
    // in this <li> tag we'll use v-for, create the character variable
    // for the characters array and output in inside {{}}
    <li v-for="character in characters">{{character}}</li>
</div>
```

To output an array with objects

```js
ninjas: [

    { name: 'Ryu', age: 25},
    { name: 'Yoshi', age: 35},
    { name: 'Ken', age: 55}

]
// we use item.key to output each object
<li v-for="ninja in ninjas">{{ninja.name}} - {{ninja.age}}</li>
```

How to output an index of an array ?

```js
<li v-for="(ninja, index) in ninjas">{{index}}. {{ninja.name}} - {{ninja.age}}</li>
```

What if we don't want to output a specific html element like a `<div>` or an `<li>` ?
We change it for `<template></template>`

To output all objects without knowing it's properties

```js
<template v-for="ninja in ninjas">

<div v-for="(val, key) in ninja">{{val}}</div>

</template>
```
