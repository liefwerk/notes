# setting_up_routing

## part 2

Routing has to be installed with a npm package

```js
npm i vue-router --save
```

Then we import it inside the main.js

`Vue.use(VueRouter)`

To setup the routes, we first create an array of objects (in another file called Route.js)

```js
import showBlogs from './components/showBlogs.vue'
import addBlog from './components/addBlog.vue'

export default [

{ path: '/', component: showBlogs },
{ path: '/add', component: addBlog },

]
```

Then we import this file in main.js

`import Routes from './Routes.js'`

we setup the routing

```js
const router = new VueRouter({

routes: Routes

})
```

and we add it in our Vue instance

```js
new Vue({

el: '#app',
render: h => h(App),
router: router

})
```
