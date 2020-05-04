# React Router

When we make a request, we make the initial request. We get a response, react looks at the response and loads a component for this request.
Only injects the component it needs to.

First, we install the package `react-router-dom`

`npm i react-router-dom`

Then, at the bottom of App.js we inject

`import {BrowserRouter, Route} from "react-router-dom"`

We create Links inside the JSX (navbar) in App.js

`<BrowserRouter></BrowserRouter>`

and we set-up the routes and attach each component to its own route.

```
<Route exact path="/" component={Home}/>
<Route path="/about" component={About}/>
<Route path="/contact" component={Contact}/>
```

The exact attribute is used when we want React to stop looking for the routes once it finds the right one for the request.
Could be useful to restart the server, that might throw an error.