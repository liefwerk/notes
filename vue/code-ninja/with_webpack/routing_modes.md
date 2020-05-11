# routing_modes

## Hash vs History

If we go to a website and go to /home, that makes a request to the server. Evey time we change the url, it makes another request.
Vue uses an # in front of the URL because it doesn't make another request to the server.

It doesn't make a request, it takes you to another place on the application.

To get rid of this, we have to setup our server.

Here's a [good guide to get started](https://router.vuejs.org/guide/essentials/history-mode.html#example-server-configurations)
*let's continue with this doc* later

Then we place the mode: 'history' or 'hash' (by default) inside our vueRouter object.

```js
const router = new VueRouter({

routes: Routes,
mode: 'history'

})
```
