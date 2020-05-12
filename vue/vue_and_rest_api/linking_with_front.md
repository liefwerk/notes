# Linking the back end to the front end

Since now we have all the files needed to handle the data, let's hook our front end and receive the data.

We'll create a `Register.vue` file to handle the registration of a user

```html
<template>
    <v-card ref="form" class="pa-md-auto mx-auto my-10" max-width="500">
      <v-card-text>
        <v-text-field
          label="Email"
          v-model="email"
        ></v-text-field>
        <br>
        <v-text-field
          label="Password"
          type="password"
          v-model="password"
          autocomplete="new-password"
        ></v-text-field>
        <br>
        <div class="danger-alert" v-html="error" />
        <br>
        <v-btn
          class="green lighten-1" dark
          @click="register">
          Register
        </v-btn>
      </v-card-text>
    </v-card>
</template>
```

```js
import AuthenticationService from '../services/AuthenticationService'
```

At the start of our script, we import a file containing different methods to send the data.
These methods are placed inside `AuthenticationService.js`

```js
// from this file we import methods using axios, they are accessible from Api.js
import Api from '@/services/Api'

// there we export the methods
export default {
  register (credentials) {
    return Api().post('register', credentials)
  },
  login (credentials) {
    return Api().post('login', credentials)
  }
}
```

Here's the content of Api.js

```js
// we import the axios package to handle the connection
import axios from 'axios'

// we export the main method using axios.create({baseUrl: 'url'})
export default () => {
  return axios.create({
    baseURL: 'http://localhost:8081/'
  })
}
```

Then inside our `Register` component, we use that the different methods to send the data to our API.

```js
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    // Here's the creation of our register method
    async register () {
      try {
        // we initiate a response with the register method from our AuthenticationService.js file
        const response = await AuthenticationService.register({
          // this method takes an object with the email and the password typed by the user
          // this object will later be known as req.body
          email: this.email,
          password: this.password
        })
        // we then dispatch these actions
        // 'setToken' and 'setUser' are stored inside the store.js file
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }
}
```

That's it, we can now try to create an account and log it in.
