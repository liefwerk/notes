# filters

If we want to filter or add functions globally to our components, we can use this method.
Very useful if we don't want to alter the original data.

First, we put our filter in the custom tag.

`<h2 v-rainbow>{{blog.title | to-uppercase}}</h2>`

Then we create a filter in the main.js file

```js
// filters
Vue.filter('to-uppercase', function(value){
    return value.toUpperCase()
})
```

## Custom Search Filter

First, we add an input with a `v-model` attribute to get it's content.

`<input type="text" v-model="search" placeholder="search blogs" />`

Then we create a new array with the search content

```js
data() {
    return {
        blogs: [],
        search: ''
    }
}
```

and inside `computed()` we create a function that will filter the blog posts we display

```js
computed: {
    filteredBlogs: function(){
        return this.blogs.filter((blog) => {
            return blog.title.match(this.search)
        })
    }
},
```

finally, we pass filteredBlog as an array in the `v-for` loop

`<div v-for="(blog, index) in filteredBlogs" :key="index" class="single-blog">`
