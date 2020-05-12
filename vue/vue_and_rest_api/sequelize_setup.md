# Intro to sequelize

## Adding the sequelize packages

Sending or getting requests is very useful, but using a specific language is better.
With NodeJS we can install a package named `sequelize` and `sqlite3`

```bash
npm install --save sequelize sqlite3
```

To setup sequelize, we have to create a model.
We'll store it inside an `index.js` in a `models` folder

```js
// index.js in ./models
// we require the different packages
const fs = require('fs')
const path = require('path')
const Sequelize = require('sequelize')
const config = require('../config/config')
// we initiate the database object
const db = {}

// here's what we'll use from Sequelize
// we store it inside a sequelize constant
const sequelize = new Sequelize(
  config.db.database,
  config.db.user,
  config.db.password,
  config.db.options
)

fs
  .readdirSync(__dirname)
  .filter((file) =>
    file !== 'index.js'
  )
  .forEach((file) => {
    const model = sequelize.import(path.join(__dirname, file))
    db[model.name] = model
  })

db.sequelize = sequelize
db.Sequelize = Sequelize

// we export the database to use it in our config file app.js
module.exports = db
```

In our `app.js` file, we add the sequelize model

```js
const { sequelize } = require('./models')
```

and bellow the other lines we construct our sequelize method.

```js
require('./routes')(app)

sequelize.sync()
.then(() => {
  app.listen(config.port)
  console.log(`server started on port ${config.port}`)
})
```

## Exporting the Routes

Notice that we also required a route folder, we'll have to create it and past our previous endpoints there.
We'll later pass Controllers inside that file.

```js
const AuthenticationController = require('./controllers/AuthenticationController')
const AuthenticationControllerPolicy = require('./policies/AuthenticationControllerPolicy')

module.exports = (app) => {
  app.post('/register',
  AuthenticationControllerPolicy.register,
  AuthenticationController.register
  )

  app.post('/login',
  AuthenticationController.login
  )
}
```

### Creating the controllers

The controllers are functions that work asynchronicaly.
Inside the `module.exports` we'll create the functions that respectively handle a `request` and a `response`.

```js
// we load the User model
const {User} = require('../models')
const jwt = require('jsonwebtoken')
const config = require('../config/config')

// that function takes the user and returns a token
// that token is only known by the server, which prevents a hacker from generating a token
function jwtSignUser (user) {
  const ONE_WEEK = 60 * 60 * 24 * 7
  return jwt.sign({data: user},
    config.authentication.jswtSecret, {
      expiresIn: ONE_WEEK
    }
  )
}

module.exports = {
  // first function that is fires when a user registers
  async register (req, res) {
    try {
      // we store the user using the create function
      const user = await User.create(req.body)
      const userJson = user.toJSON()
      // we send the data to the SQL database
      res.send({
        user: userJson,
        // we use a token instead of the password
        token: jwtSignUser(userJson)
      })
    } catch (err) {
      res.status(400).send({
        error: 'This email account is already in use.'
      })
    }
  },
  // this is the login function
  async login (req, res){
    try {
      const {email, password} = req.body
      const user = await User.findOne({
        where: {
          email: email
        }
      })
      if (!user) {
        res.status(403).send({
          error: 'The login information was incorrect'
        })
      }

      const isPasswordValid = await user.comparePassword(password)
      if (!isPasswordValid) {
        res.status(403).send({
          error: 'The login information was incorrect'
        })
      }

      const userJson = user.toJSON()
      res.send({
        user: userJson,
        token: jwtSignUser(userJson)
      })
    } catch (err) {
      res.status(500).send({
        error: `${err}, an error has occured trying to login`
      })
    }
  }
}
```

### Creating the User model

This model includes a crypting method using `bcryptjs` and `bluebird`.

```js
const Promise = require('bluebird')
const bcrypt = Promise.promisifyAll(require('bcryptjs'))

// here we initiate a function to check if the password has changed
// and to return the hashed password
function hasPassword (user) {
  const SALT_FACTOR = 8

  if (!user.changed('password')){
    return;
  }

  return bcrypt
  .genSalt(SALT_FACTOR)
  .then(salt => bcrypt.hash(user.password, salt, null))
  .then(hash => {
    user.setDataValue('password', hash)
  })
}

// there we export the models
module.exports = (sequelize, DataTypes) => {
  // the User model is setup here
  // it takes two objects, email and password
  const User = sequelize.define('User', {
    email: {
      type: DataTypes.STRING,
      unique: true
    },
    password: DataTypes.STRING
  }, {
    // we choose to hook it here
    hooks: {
      beforeSave: hasPassword
    }
  })

  // here a prototype function to compare the passwords
  User.prototype.comparePassword = function (password) {
    return bcrypt.compare(password, this.password)
  }

  // there we finally return the user object with the email and hashed password
  return User
}
```
