# mixins

It's some code that we can reuse over and over.
Good way to externalize the bit of code.

Firstly, we export the bit of code inside another js file

```js
export default {
    computed: {
        filteredBlogs: function(){
            return this.blogs.filter((blog) => {
                return blog.title.match(this.search)
            })
        }
    }
}
```

Then we import it inside the components in which we want to use it

`import searchMixin from '../mixins/searchMixin'`

and we place it after the methods in `export default`

```js
export default {

data() {
// datas},
mixins: [searchMixin]
```
