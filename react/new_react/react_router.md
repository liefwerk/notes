# React router

The way to have multiple pages, we use the `React Router`.

A typical website gets a request from an url and then handles it. Generally it will send back an `HTML` page. In the case of a SPA, it start the same but the server also sends back a js bundle. The initial `index.html` is empty, then React populates it with Javascript. On the next request, React intercepts it and routes it to other views.

## Router setup

First step is to install it as a package: `npm install react-router-dom@5`. We then travel to our `App.js` file and import a few things:

```javascript
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
```

We can now return the following code to setup our `Routes`:

```javascript
<Router>
    <divclassName="App">
        <Navbar/>
        <div className="content">
            <Switch>
                <Route path="/">
                    <Home/>
                </Route>
            </Switch>
        </div>
    </div>
</Router>
```

## Exact match routes

Let's try adding another route. Let's make a new component called `Create`.

After importing it in out `App` component and adding it to the Route, we see that when we go to `/create` it also loads the homepage component.That is because React sees the first route inside the second one. The way to only get one component at a time is to use the key `exact` before our `path` inside the `<Route>` tag: `<Route exact path="/">`.

## Router links

We've set up different routes but when we click through them we keep sending a request and it still reloads the page. To let Rect intercept the request we need to use the special `<Link>` tag.