# My account page

Let's first create our view.

```html
<template>
  <div class="my-page-account">
    <div class="columns is-multiline">
      <div class="column is-12">
        <h1 class="title">My account</h1>
      </div>
      <div class="column is-12">
        <button @click="logout()" class="button is-danger">Log out</button>
      </div>
    </div>
  </div>
</template>
```

Then, let's add the `logout` function we linked to the `Log out` button.

```javascript
<script>
export default {
  name: 'MyAccount',
  methods: {
    logout(){
      axios.defaults.headers.common["Authorization"] = ""

      localStorage.removeItem("token")
      localStorage.removeItem("username")
      localStorage.removeItem("userid")

      this.$store.commit('removeToken')

      this.$router.push('/')
    }
  }
}
</script>
```

Now head to the router `index.js` file. To prevent the user from accessing the `My account` page without being logged in, let's add a router guard. 

```javascript
import store from '../store'
import MyAccount from '../views/MyAccount.vue'

...

const routes = [
    ...
    {
    path: '/my-account',
    name: 'MyAccount',
    component: MyAccount,
    // the router guard
    meta: {
      requireLogin: true
    }
  },
```

The router guard doesn't work without adding new rules at the bottom of this file.

```javascript
router.beforeEach((to, from, next) => {
  // if the route finds that requireLogin is set to true
  // and the user is not authenticated
  if (to.matched.some(record => record.meta.requireLogin) && !store.state.isAuthenticated) {
    // redirect to the login page
    next({ name: 'LogIn', query: { to: to.path } });
  } else {
    // else follow the route
    next()
  }
})
```

Now is the user is authenticated and goes to the `/my-account` page, it will work. Otherwise, the redirections will bring the user to the `/log-in` page.

Let's say that the suer logs in and now wants to visit its `/my-account` page. The best way to make the page available to him is to replace the current `Log in` button in the navigation with a `My account` button.

Go to `App.vue` and add the following code just before the cart button in the template.

```html
<template v-if="$store.state.isAuthenticated">
    <router-link to="/my-account" class="button is-light">My account</router-link>
</template>

<template v-else>
    <router-link to="/log-in" class="button is-light">Log in</router-link>
</template>
```