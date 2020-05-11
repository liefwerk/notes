# routing_links

## Adding Routing Links

In a template we create a place for our navigation and we import it to our root component.

```html
<nav>
  <ul>
    <li><router-link to="/" exact>Blog</router-link></li>
    <li><router-link to="/add" exact>Add a blog post</router-link></li>
  </ul>
</nav>
```

The attribute exact tells Vue that we want the exact path, which helps with some rules siuch as the active styling in the menu links.

## Route Params

If we have a blog, having a few posts your URL would look like this `/blog/123` or `/blog/:id`
`:id` is a route parameter

First we setup a Route

`{ path: 'blog/:id', component: singleBlog }`

In the singleBlog component we'll then detect the parameter and handle it by making a http request for the correct ressource.

```html
<template>

<div id="single-blog">
  <h1>{{blog.title}}</h1>
  <article>{{blog.body}}</article>
</div>

</template>
```

```js
export default {
  data() {
    return {
      id: this.$route.params.id,
      blog: {}
    }
  },
  created(){
    const axios = require('axios');
      axios.get('https://jsonplaceholder.typicode.com/posts/' + this.id, { crossdomain: true })
      .then(data => {
        this.blog = data.data
      }
    )
  }
}
```

And finally, in showBlogs we wan add a `<router-link>` tag to the title of each blog post

`<router-link :to="'/blog/' + blog.id"><h2>{{blog.title | to-uppercase}}</h2></router-link>`
