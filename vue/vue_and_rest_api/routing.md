# Routing with Vue Router

Routing in a Vue application means redirecting users to differents pages.

To use it, we first need to install it with npm

```bash
npm install vue-router
```

We create a new folder named `router` with an `index.js` file inside.
Here's an example of setup for this router file

```js
import Vue from 'vue'
import Router from 'vue-router'
import Home from '@/components/Home'
import Login from '@/components/Login'
import Register from '@/components/Register'

// we tell Vue to use Router
Vue.use(Router)

// we export our router to later use it inside our vue instance
export default new Router({
  routes: [
    // the routes array takes objects
    {
      // we tell the path
      path: '/',
      // it's name
      name: 'root',
      // and the (parent) component that we want to show
      component: Home
    },
    {
      path: '/login',
      name: 'login',
      component: Login
    },
    {
      path: '/register',
      name: 'register',
      component: Register
    }
  ]
})

```

Then, inside our main.js file, we import the routing parameters

```js
import router from './router'
```

and we add them to our vue instance

```js
new Vue({
  router,
  render: h => h(App)
}).$mount('#app')
```
