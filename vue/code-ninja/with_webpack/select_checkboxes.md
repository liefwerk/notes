# select_checkbox

## Binding Checkboxes

First we create the input with `type="checkbox"` and `v-model="blog.categories"`

```html
<label>Ninjas</label>
<input type="checkbox" value="ninjas" v-model="blog.categories">
<input type="checkbox" value="mario" v-model="blog.categories">
```

Then we create the data array

```js
data() {
    return {
        blog: {
            title: "",
            content: "",
            categories: []
        }
    }
}
```

and we output it

```html
<ul>
    <li v-for="(categorie, index) in blog.categories" :key="index">{{categorie}}</li>
</ul>
```

## Selectbox Binding

First we creat the label

```html
<label>Author</label>

<select v-model="blog.author">
<option v-for="(author, index) in authors" :key="index">{{author}}</option>

</select>


// then we output the data inside a v-for loop
<ul>

<li v-for="(categorie, index) in blog.categories" :key="index">{{categorie}}</li>

</ul>
<p>Author: {{blog.author}}</p>

```

Then we create the data array

```js
data() {
  return {
    blog: {
      title: "",
      content: "",
      categories: [],
      author: ""
  },
  authors: ['The Net Ninja', 'The Angular Avenger', 'The Vue Vindicator']
  }
}
```
