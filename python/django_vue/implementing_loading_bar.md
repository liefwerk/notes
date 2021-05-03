# Implementing a loading bar

Let's learn how to show a loading bar when the request takes time.

## Adding a new mutation

Go to `store/index.js` and add a new mutation.

```javascript
setIsLoading(state, status) {
    state.isLoading = status
}
```

Now in `Product.vue` at the top of the function called `getProduct()` we add:

```javascript
// we add async/await because this is now an asynchronous task
async getProduct(){
    // here we call the event setIsLoading and return true
    this.$store.commit('setIsLoading', true)

    const category_slug = this.$route.params.category_slug
    const product_slug = this.$route.params.product_slug

    await axios
        .get(`/api/v1/products/${category_slug}/${product_slug}`)
        .then(response => {
            this.product = response.data
        })
        .catch(error => {
            console.log(error)
    })

    // here we call the event setIsLoading and return false
    this.$store.commit('setIsLoading', false)
},
```

## Adding the loading bar

Go to `App.vue` and after the `<nav></nav>` section we create a new `div`.

```html
<div class="is-loading-bar has-text-centered" :class="{ 'is-loading': $store.state.isLoading }">
    <div class="lds-dual-ring"></div>
</div>
```

Let's also add some styling:

```css
<script lang="scss">
...
.lds-dual-ring {
  display: inline-block;
  width: 80px;
  height: 80px;
}

.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #ccc;
  border-color: #ccc transparent #ccc transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}

@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.is-loading-bar {
  height: 0;
  overflow: hidden;
  -webkit-transition: all 0.3s;
  transition: all 0.3s;

  &.is-loading {
    height: 80px;
  }
}
```

## Adding the loading bar to other places

Any place that fetches data can emit the action, just remember to add async/await to your function.

```javascript
methods: {
    async getLatestProducts() {
        // setting loading to true
        this.$store.commit('setIsLoading', true)
        // fetching the data
        await axios
            .get('/api/v1/latest-products/', { crossdomain: true })
            .then(response => {
                console.log(response.data)
                this.latestProducts = response.data
            })
            .catch(error => {
                console.log(error)
            })
        // setting loading to false
        this.$store.commit('setIsLoading', false)
    }
}
```