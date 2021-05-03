# Adding search functionality

## Adding a new view in the back end

Go to `views.py` and import `decorators` from the Django framework.

```python
from django.db.models import Q
...
from rest_framework.decorators import api_view

# we just want to accept post requests to this view
@api_view(['POST'])
def search(request):
    # we want to receive the query
    query = request.data.get('query', '')

    if query:
        # we check if the name OR the description contains the query
        products = Product.objects.filter(Q(name__icontains=query) | Q(description__icontains=query))
        # we pass in the product in our serializer
        serializer = ProductSerializer(products, many=True)
        return Response(serializer.data)
    else:
        return Response({"products": []})
```

Now import this to the URLs in `product/urls.py`.

```python
urlpatterns = [
    path('latest-products/', views.LatestProductsList.as_view()),
    path('products/search/', views.search),
    ...
]
```

## Dealing with the front end

### Adding the search bar HTML

Let's go to `App.vue`. Below the `.navbar-menu` div, add the following `HTML`.

```html
<div class="navbar-start">
    <div class="navbar-item">
        <form method="get" action="/search">
            <div class="field has-addons">
                <div class="control">
                    <input type="text" class="input" placeholder="What are you looking for?" name="query">
                </div>

                <div class="control">
                    <button class="button is-success">
                        <span class="icon">
                            <i class="fas fa-search"></i>
                        </span>
                    </button>
                </div>
            </div>
        </form>
    </div>
</div>
```

### Creating a new view

Create a new file called `Search.vue`. In the template part, paste this code.

```html
<template>
  <div class="page-search">
    <div class="columns is-multiline">
      <div class="column is-12">
        <h1 class="title">Search</h1>
        <h2 class="is-size-5 has-text-grey">Search term: "{{query}}"</h2>
      </div>

      <ProductBox 
        v-for="product in products"
        :key="product.id"
        :product="product"
      />
    </div>
  </div>
</template>
```

In the script part, use this piece of code.

```javascript
<script>
import axios from 'axios'
import ProductBox from '@/components/ProductBox.vue'

export default {
  name: 'Search',
  components: {
    ProductBox
  },
  data() {
    return {
      products: [],
      query: ''
    }
  },
  mounted() {
    document.title = 'Search | Djackets'
  }
}
</script>
```

Next step is to import the view in the router `index.js` file.

```javascript
import Search from'../views/Search.vue'

const routes = [
...
{
    path: '/search',
    name: 'Search',
    component: Search
},
]
```

Before fetching the right products via axios, the query needs to be extracted from the URL. In the `mounted` section of our `Seach.vue` file, let's add a function called `performSearch`.

```javascript
mounted() {
    document.title = 'Search | Djackets'

    let url = window.location.search.substring(1)
    let params = new URLSearchParams(url)

    if (params.get('query')){
      this.query = params.get('query')

      this.performSearch()
    }
}, methods: {
    performSearch() {

    }
}
```

Let's update our `performSearch` function with some axios logic to fetch the data from the server.

```javascript
async performSearch() {
      this.$store.commit('setIsLoading', true)

      await axios
        .post('/api/v1/products/search/', {'query': this.query})
        .then(response => {
          this.products = response.data
        })
        .catch(error => {
          console.log(error)
        })

      this.$store.commit('setIsLoading', false)
    }
```