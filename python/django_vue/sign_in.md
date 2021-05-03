# Creating the Sign In for our application

The Log In page will be very similar to the Sign Up page.

```javascript
<template>
  <div class="page-sign-up">
    <div class="columns">
      <div class="column is-4 is-offset-4">
        <h1 class="title">Log in</h1>

        <form @submit.prevent="submitForm">
          <div class="field">
            <label>Username</label>
            <div class="control">
              <input type="text" class="input" v-model="username">
            </div>
          </div>
          <div class="field">
            <label>Password</label>
            <div class="control">
              <input type="password" class="input" v-model="password">
            </div>
          </div>
          <div class="notification is-danger" v-if="errors.length">
            <p v-for="error in errors" :key="error">{{error}}</p>
          </div>
          <div class="field">
            <div class="control">
              <button class="button is-dark">Log in</button>
            </div>
          </div>
          <hr>
          
          Or click here to <router-link to="/sign-up">sign up</router-link>!
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
 
export default {
  name: 'LogIn',
  data(){
    return {
      username: '',
      password: '',
      errors: [],
    }
  },
  mounted(){
    document.title = 'Log in | Djackets'
  }
}
</script>
```

In the `index.js` from the `store` folder, below the `initializeStore`, add the following code. This is to check if there already is an item named `token` in the `localStorage`.

```javascript
if (localStorage.getItem('token')) {

    state.token = localStorage.getItem('token')

    state.isAuthenticated = true

  } else {

    state.token =''

    state.isAuthenticated = false

  }if (localStorage.getItem('token')) {
    state.token = localStorage.getItem('token')
    state.isAuthenticated = true
  } else {
    state.token = ''
    state.isAuthenticated = false
  }
```

Below, in `mutations`, let's add two functions to `set` and `delete` the token.

```javascript
...
setToken(state, token) {
  state.token = token
  state.isAuthenticated = true
},
removeToken(state) {
  state.token = ''
  state.isAuthenticated = false
},
```

In `App.vue`, let's setup the token in the `beforeCreate` hook.

```javascript
beforeCreate() {
    // this verifies if we already have a token
    this.$store.commit('initializeStore')
    const token = this.$store.state.token
    // if there is one add auth
    if (token) {
        axios.defaults.headers.common['Authorization'] = "Token " + token
    } else {
        axios.defaults.headers.common['Authorization'] = ""
    }
  },
```

In `LogIn.vue`, below the mounted create a new `submitForm` function to handle the token creation.

```javascript
methods: {
    async submitForm() {
      // by defaults, remove the current auth
      axios.defaults.headers.common["Authorization"] = ""
      // by defaults, also remove the current token from local storage
      localStorage.removeItem("token")

      // construct the data from the form
      const formData = {
        username: this.username,
        password: this.password,
      }

      await axios
        // in the login url from the backend, end the data
        .post("/api/v1/token/login/", formData)
        .then(response => {
          const token = response.data.auth_token
          // sending event to the store to set the token
          this.$store.commit('setToken', token)
          // telling the headers our new token
          axios.defaults.headers.common["Authorization"] = "Token " + token
          // saving the token in the localstorage
          localStorage.setItem("token", token)
          // redirecting to either the previous url or the cart url
          const toPath = this.$route.query.to || '/cart'
          // redirecting
          this.$router.push(toPath)
        })
        .catch(error => {
          // handling errors
          if (error.response){
            for (const property in error.response.data){
              this.errors.push(`${property}: ${error.response.data[property]}`)
            }
          } else {
            this.errors.push('Something went wrong. Please try again!')

            console.log(JSON.stringify(error))
          }
        })
    }
}
```