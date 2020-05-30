# Initialization of the project

We'll create a REST API with Postgresql and NodeJS.

## The main folder structure

The first step is to create our main folder and place this document structure:

```bash
- __portfolio__
   - __main__
     - [README.md](main/README.md)
     - [babel.config.js](main/babel.config.js)
     - [node\_modules](main/node_modules)
     - [package\-lock.json](main/package-lock.json)
     - [package.json](main/package.json)
     - __public__
       - [favicon.ico](main/public/favicon.ico)
       - [index.html](main/public/index.html)
     - __src__
       - [App.vue](main/src/App.vue)
       - __assets__
       - __components__
         - [HelloWorld.vue](main/src/components/HelloWorld.vue)
         - [Home.vue](main/src/components/Home.vue)
       - __controllers__
       - [index.js](main/src/index.js)
       - [main.ts](main/src/main.ts)
       - __routes__
       - [shims\-tsx.d.ts](main/src/shims-tsx.d.ts)
       - [shims\-vue.d.ts](main/src/shims-vue.d.ts)
       - __store__
         - [index.ts](main/src/store/index.ts)
     - [tsconfig.json](main/tsconfig.json)
```

The important part is the following structure:

```bash
     - __src__
       - __controllers__
       - [index.js](main/src/index.js)
       - __routes__
```

## Installation of packages

We'll install two packages to help us access Postgresql.
`express` will give us a way to create the server, receive the data, etc..
`pg` will help us to create a connection to our database.

```bash
npm i express pg --save
```

## Setup of the packages

Let's go to our `index.js` file in the `src` folder

```js
const express = require("express");
const app = express();

app.listen(3000);
console.log("Server on port 3000");
```

If we go to `localhost:3000` it gives us an error. This is because we don't have any route telling us where to land.
The solution is to create an `index.js` in the `routes` folder.

```js
const { Router } = require("express");
const router = Router();

module.exports = router;
```

Then we'll add it to our `src/index.js`

```js
app.use(require("./routes/index"));
```

Because we'll have to understand the data passing through, we'll add some middlewares.
Middlewares are functions that happend before the routing.

```js
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
```

Now let's go back to our routes folder and add our first route.

```js
router.get("/users", (req, res) => {
  res.send("users");
});
```

## Adding nodemon

There is a packages called `nodemon` that helps us to auto-restart our server.
Let's add it and also add a new script to us it in `packages.json`.

```bash
npm i nodemon -D
```

Then let's add this script in `packages.json`:

```js
"dev": "nodemon src/index.js";
```

To clean up our code, we'll export the router function and place it inside an `index.controllers.js` file in the `controllers` folder.

```js
const getUsers = (req, res) => {
  res.send("users");
};

module.exports = {
  getUsers,
};
```

Then we'll import it in our `routes/index.js` file

```js
const { getUsers } = require("../controllers/index.controllers");

router.get("/users", getUsers);
```

Now we can go to `localhost:3000/users` and we'll get the text `users` that we defined in our getUsers constant.
