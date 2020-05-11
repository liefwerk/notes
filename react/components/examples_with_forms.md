# Example with Forms

## An example

```js
// We import React
import React, { Component } from "react"

// Because we'll use datas from other components we'll make it as a class and not a function
class AddNinja extends Component {

// declaration of the state with the data inside
state = {
    name: null,
    age: null,
    belt: null
}

// fonction handlechange that fires setState each time there's a change. Later on we'll use Redux to do that.
handleChange = (e) => {
    this.setState({
        [e.target.id] : e.target.value
    })
}

// fonction handleSubmit qui évite la recharge de la page et log le résultat
handleSubmit = (e) => {
    e.preventDefault();
    console.log(this.state);
}

// the render method
render(){
    return (
        <div>
            <form onSubmit={this.handleSubmit}>
                <label htmlFor="name">Name:</label>
                <input type="text" id="name" onChange={this.handleChange} />
                <label htmlFor="name">Age:</label>
                <input type="text" id="age" onChange={this.handleChange} />
                <label htmlFor="name">Belt:</label>
                <input type="text" id="belt" onChange={this.handleChange} />
                <button>Submit</button>
            </form>
        </div>
    )}
}

// let's not forget to export the Component/class
export default AddNinja
```
