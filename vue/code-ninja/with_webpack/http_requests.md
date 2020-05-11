# http_requests

## How to communicate with a database

First, we download the axios package with npm

`npm install @nuxtjs/axios`

then we import it to the main.js file

```js
import axios from 'axios'

// axios setup
Vue.prototype.$http = axios;
```

and we create a function that will post some data in JSON format.
Here's an example with the `post()` request

```js
methods: {

post: function(){
const axios = require('axios');

axios.post('https://jsonplaceholder.typicode.com/posts', {
title: this.blog.title,
body: this.blog.content,
userId: 1
}).then(data => {
console.log(data);
this.submitted = true
})
}

}
```

and there, an example with the `get()` request - we'll place it inside the `created()` lifecycle.

```js
methods: {},
created(){

const axios = require('axios');
axios.get('https://jsonplaceholder.typicode.com/posts', { crossdomain: true })
.then(data => {
this.blogs = data.data.slice(0, 10)
})

}
```
