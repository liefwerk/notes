# Props

## What are props

Way to pass data from one component to another one.

Under `render`

`const{name,age,belt}=this.props;`

then, we replace the variables inside a div as JSX.

`<div>Name:{name}</div>`

This way, it's possible to print the same component with different data.

## Outputting Lists

First, in the main JS file, before render, we have to make a function called state

```js
state = {
   ninjas: [
        { name: 'Ryu', age: 30, belt:'black', id: 1 },
        { name: 'Yoshi', age: 20, belt: 'green', id: 2 },
        { name: 'Crystal', age: 25,belt: 'pink',id: 3 }
    ]
}
```

and call the component in the HTML this way

`<Ninjas ninjas = { this.state.ninjas } />`

In the App JS file, we get the array create in the main JS file and make it a props:

`const {ninjas} = this.props;`

Then we create an array and map this array into it:

```js
const ninjaList = ninjas.map(ninja => {

return(
    <div className="ninja" key={ninja.id}>
        <div>Name:{ninja.name}</div>
        <div>Age:{ninja.age}</div>
        <div>Belt:{ninja.belt}</div>
    </div>
    )
})
```

Finally, we return the list in the HTML as a dynamic JS code:

```js
return(
    <divclassName="ninja-list"> {ninjaList} </div>
)
```
