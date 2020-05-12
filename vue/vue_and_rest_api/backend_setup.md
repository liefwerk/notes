# Backend setup

## Setup of the project

Since we want to interact with a REST API, our best choice would be to include a backend server in our setup.

Next to our client folder, we'll create a server folder.
From the terminal, we'll initiate a npm project inside that folder, in order to have the package.json file.

```bash
npm init -f
```

## Installation of Nodemon and Eslint

Then we'll install two packages: **nodemon** and **eslint**.
**Nodemon** is a utility that will monitor for any changes in your source and automatically restart your server. Perfect for development.
**Eslint** is a tool for identifying and reporting on patterns found in ECMAScript/JavaScript code. That will help us clean our code.

```bash
npm install --save nodemon eslint
```

### Script setups

Inside the package.json folder we'll add two scripts to easily launch the nodemon and eslint scripts.

```js
"scripts": {
    "start": "./node_modules/nodemon/bin/nodemon.js src/app.js --exec 'npm run lint && node'",
    "lint": "./node_modules/.bin/eslint \"**/*.js\""
},
```

Then we create a `src` folder with an `app.js` file inside.

We write a simple console code to check that it runs.

```js
console.log('hello world')
```

### Initialisation of eslint

In order to launch eslint, we have to initiate it. To to that, we'll use the terminal, find the path to eslint.js and run the --init command.

```bash
node ./node_modules/eslint/bin/eslin.js --init
```

We then choose the options that we like.
Once it is initiated, we can finally run our `npm start` script.

```bash
npm start
```

## More backend packages

We'll install 4 other packages to handle the API connection between the font and back-end

```bash
npm install --save express body-parser cors morgan
```

Then we set them up in our `app.js` file

```js
const express = require('express')
const bodyParser = require('body-parser')
const cors = require('cors')
const morgan = require('morgan')

const app = express()
app.use(morgan('combined'))
app.use(bodyParser.json())
app.use(cors())

app.get('/status', (req, res) => {
  res.send({
    message: 'hello world!'
  })
})

app.listen(process.env.PORT || 8081)
```

The `app.get()` methods is a GET request.
This means that when a user will send a get request to our `/status` endpoint, they will receive the message `hello world`.
