# Functions as Props

First, we create a function called `addNinja()`
Then we import the file addNinja.js with the function inside

```js
import AddNinja from './components/addNinja.js
```

Then we place that component as a tag `<addNinja />` inside the render method to show it on the HTML.
Inside the tag we add an attribute `addNinja =` with the props inside `{ this.addNinja }`

`<AddNinja addNinja = { this.addNinja } />`

Important, if we touch an array and want to add or delete, the best way is to copy it with the spread operator [...array]

`let ninjas = [...this.state.ninjas, ninja];`

Then we pass it as the state of the Component

```js
this.setState({ ninjas: ninjas })

// if the new props have the same name, it is possible to do it this way
this.setState({ ninjas })
```
