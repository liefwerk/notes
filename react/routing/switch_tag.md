# Switch Tag

It is a tag to load in App.js around the Route parameters.

First we import it as a function from `react-router-dom`:

`import {BrowserRouter, Route, Switch} from "react-router-dom"`

Then we wrap the `<Route/>` tags with `<Switch>` and `</Switch>`

What this does is when React checks the Routes, it will stop at the first one that is equal to the request. It will not continue.
