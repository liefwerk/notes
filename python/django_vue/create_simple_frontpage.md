# Create a simple front page for the latest products

We can go back to vue and construct a new view for our latest products.

## Creating the HTML structure

Let's first head to `Home.vue` and add some HTML to the template.

```html
<section class="hero is-medium is-dark mb-6">
  <div class="hero-body has-text-centered">
    <p class="title mb-6">
      Welcome to Djackets
    </p>
    <p class="subtitle">
      The best jacket store online
    </p>
  </div>
</section>
```

Then below we'll create the HTML for listing all the latest products.

```html
<div class="columns is-multiline">
  <div class="column is-12">
    <h2 class="is-size-2 has-text-centered">Latest products</h2>
  </div>
  <div
    class="column is-3"
    v-for="product in lastestProducts"
    :key="product.id"
  >
    <div class="box">
      <figure class="image mb-4">
        <img :src="product.get_thumbnail">
      </figure>

      <h3 class="is-size-4">{{ product.name }}</h3>
      <p class="is-size-6 has-text-grey">${{product.price}}</p>

      View details
    </div>
  </div>
</div>
```

## Fetching the products

To fetch the product we'll use `axios`.  We first need to import it in our `<script></script>`  tag: `import axios from 'axios'` Then in our main export function well add this bit of code.

```javascript
export default {
  name: 'Home',
  // Here we define our main array latestProducts
  data() {
    return {
      latestProducts: []
    }
  },
  components: {},
  // we call the fetching function when the component is mounted
  mounted() {
    this.getLatestProducts()
  },
  // here we define the fetching function
  methods: {
    getLatestProducts() {
      axios
        // our path is setup here
        .get('/api/v1/latest-products/')
        .then(response => {
          // when it is fetched we store it inside our array
          this.latestProducts = response.data
        })
        .catch(error => {
          // if there is an error it will be logged to the console
          console.log(error)
        })
    }
  }
}
```

For now the path defined in axios isn't right, to set it up we edit the `main.js` file by adding these few lines of code.

```javascript
import axios from 'axios'

// our main url for axios
axios.defaults.baseURL = 'http://localhost:8000'

// here we simply add axios after the router
createApp(App).use(store).use(router, axios).mount('#app')
```

We can test the fetching by going to the url `http://localhost:8080/`. You might get the following error: `Cross-Origin Request BlockedCross-Origin Request Blocked`. This means that you probably didn't properly configure your CORS header.

You can go to the `settings.py` file in the main django folder and add the missing url in the `CORS_ALLOWED_ORIGINS` list.

```python
CORS_ALLOWED_ORIGINS = [
    "http://localhost:8000",
    "http://localhost:8080",
]
```