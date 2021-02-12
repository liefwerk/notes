# Adding styles

How do we add CSS to our components ?
We have an `app.css` file that is applied globally. How do we limit the scope to only one component ?

## Adding style with an external file

We'll delete the` app.css` file and its `import` and create an `index.css` file. This will be our external `.css` file. We ca then write any CSS we want inside.

## Adding style inline

It also is possible to add `inline` style. Let's go to our `Navbar.js` file and add a new `style` tag to the JSX.

```javascript
<a href="/create" style = {{

color: 'white',
backgroundColor: '#f1356d',
borderRadius: '8px'

}}>New Blog</a>
```