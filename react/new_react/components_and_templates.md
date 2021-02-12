# Components and templates

Components are the building blocks of any React application. A web page can be made of multiple components instances. An article might be a component, a sidebar too.

Each component has a template and a logic. A navbar will have a HTML template and a logic when we click on a menu for example.

## The root component

At the start of any project, only one component is created and active: `App.js`. All it's content is being rendered on the browser. This is known as a root component.

Inside this component there is a function called `App` that returns some HTML code. This piece of HTML is called JSX, it is then converted with babel and is built on the browser. One big difference with JSx and HTML, we use attributes with `camelCase` like `className`.

### Initialazing the root component

To initialise the root component we'll return this piece of JSX:

```javascript
<div className="App">
    <div className="content">
        <h1>App Component</h1>
    </div>
</div>
```

### Exporting the component

At the end of a component we always export it to use in another file: `export default App;`.

Then we import it in another file: `import 'App' from ./App;`.

