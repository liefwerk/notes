# Creating the Sign Up for our application

First, create a new view for the page by creating `SignUp.vue`.

```html
<template>
  <div class="page-sign-up">
    <div class="columns">
      <div class="column is-4 is-offset-4">
        <h1 class="title">Sign up</h1>
      </div>
    </div>
  </div>
</template>
```

```javascript
<script>
import axios from 'axios'
import {toast} from 'bulma-toast'
 
export default {
  name: 'SignUp',
  data(){
    return {
      username: '',
      password: '',
      password2: '',
      errors: [],
    }
  }
}
</script>
```

As usual, the next step is to import it to the router.

Now let's add a new form to our `template`.

```html
<template>
  <div class="page-sign-up">
    <div class="columns">
      <div class="column is-4 is-offset-4">
        <h1 class="title">Sign up</h1>

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
          <div class="field">
            <label>Repeat password</label>
            <div class="control">
              <input type="password" class="input" v-model="password2">
            </div>
          </div>
          <div class="notification is-danger" v-if="errors.length">
            <p v-for="error in errors" :key="error">{{error}}</p>
          </div>
          <div class="field">
            <div class="control">
              <button class="button is-dark">Sign up</button>
            </div>
          </div>
          <hr>
          
          Or click here to <router-link to="/log-in">log in</router-link>!
        </form>
      </div>
    </div>
  </div>
</template>
```

```javascript
methods: {
    submitForm(){
      // reinitialising in case the page the user tries to log in multiple times
      this.errors = []

      // checkings for errors
      if (this.username === ''){
        this.errors.push('The username is missing')
      }

      if (this.paswword === ''){
        this.errors.push('The paswword is too short')
      }

      if (this.password !== this.password2){
        this.errors.push('The passwords don\'t match')
      }
      
      // if no errors
      if (!this.errors.length){
        // we load the data from the form
        const formData = {
          username: this.username,
          password: this.password,
        }
        
        // we pass the data to our back end url /users/
        axios
          .post("/api/v1/users/", formData)
          .then(() => {
            // we launch a toast to tell the users its account has been successfully created
            toast({
              message: 'Account created, please log in!',
              type: 'is-success',
              dismissible: true,
              pauseOnHover: true,
              duration: 2000,
              position: 'bottom-right',
            })
            
            // we redirect the user to the log in page
            this.$router.push('/log-in')
          }).catch(error => {
            // if there is an issue
            if (error.response) {
              for (const property in error.response.data){
                this.errors.push(`${property}: ${error.response.data[property]}`)
              }

              console.log(JSON.stringify(error.response.data))
            } else if (error.message){
              this.errors.push('Something went wrong. Please try again!')

              console.log(JSON.stringify(error))
            }
          })
      }
    }
}
```