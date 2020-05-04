# Single Page Apps

One one page served to the browser from the server. We only update the content delivered to the user.
React takes over the app before it reaches the server.

**Types of files**

In the folder /src we create another folder js/components. Inside, we put the file App.js
This is the Root Component.

```
import React, {Component} from "react";
import ReactDOM from "react-dom";

class App extends Component{
    render(){
        return(
            <divclassName="App">
                <h1>WelcometoReact</h1>
                <p>Welcome!</p>
            </div>
        )
    }
}

exportdefaultApp;

// we could also place this inside the index.js
const wrapper = document.getElementById("root");

// that's a turnary operator !!
wrapper ? ReactDOM.render(<App/>, wrapper) : false;

```

**Nesting Components**

We have to nest the others components inside the root component.
We can switch these components.

```
import React, { Component } from 'react'

classNinjas extends Component {
    render(){
        return(
            <div className="ninja">
                <div>Name:Ryu</div>
                <div>Age:30</div>
                <div>Belt:Black</div>
            </div>
        )
    }
}

exportdefaultNinjas
```

Inside the App.js:

`importNinjasfrom"./Ninjas"`

and inside the HTML of App.js:

`<Ninjas/>`