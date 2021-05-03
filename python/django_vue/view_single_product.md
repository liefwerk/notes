# View a single product page

Our next step is to create a detail page for a single product in which we'll show more information about our product.

## Create a new viewset in Django

We go back to `views.py` to create a new class called `ProductDetail(APIView)`

```python
class ProductDetail(APIView):
  # this function gets the object from the Product class
  # and we filter the result by the product slug and the category
  def get_object(self, category_slug, product_slug):
    try:
      return Product.objects.filter(category__slug=category_slug).get(slug=product_slug)
    except Product.DoesNotExist:
      raise Http404

  # this function gets the object, gets the product fields and returns it as a Http response
  def get(self, request, category_slug, product_slug, format=None):
    product = self.get_object(category_slug, product_slug)
    # we also want all the fields
    serializer = ProductSerializer(product)
    return Response(serializer.data)
```

Next we'll add a new path to our product api urls

```python
urlpatterns = [
  ...
  path('products/<slug:category_slug>/<slug:product_slug>/', views.ProductDetail.as_view()),
]
```

## Creating the view/vue page for showing the details

Let's go to the vue folder, into the `views` folder and create a new file called `Product.vue`.
We'll first populate the `<template></template>` tag with our HTML structure.

```html
<template>
  <div class="page-product">
    <div class="columns is-multiline">
      <div class="column is-9">
        <figure class="image mb-6">
          <img :src="product.get_image">
        </figure>
        <h1 class="title">{{ product.name }}</h1>
        <p>{{ product.description }}</p>
      </div>
      <div class="column is-3">
        <h2 class="subtitle">Information</h2>

        <p><strong>Price:</strong>${{ product.price }}</p>

        <div class="field has-addons mt-6">
          <div class="control">
            <input type="number" class="input" min="1" v-model="quantity">
          </div>

          <div class="control">
            <a class="button is-dark">Add to cart</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
```

Then we import axios, add the two variables `product` for storing the details and `quantity` for later adding to cart.

```javascript
<script>
import axios from 'axios'

export default {
  name: 'Product',
  data() {
    return {
      product: {},
      quantity: 1
    }
  },
  mounted() {
    this.getProduct()
  },
  methods: {
    getProduct(){
      const category_slug = this.$route.params.category_slug
      const product_slug = this.$route.params.product_slug
    }
  }
}
</script>
```

Let's check our router in vue in the `router` folder and `index.js` file. In this file we can see that we currently only have two paths, let's add a new one for our product view.

```javascript
import Product from'../views/Product.vue'

...

const routes = [
  ...,
  {
    path: '/:category_slug/:product_slug',
    name: 'Product',
    component: Product
  },
]
```

To access this view, we'll replace the `View details` text by a button with a link to it's url. Just go to `Home.vue`, inside the `<template></template>` tag.

```html
...
<router-link :to="product.get_absolute_url" class="button is-dark mt-4">View details</router-link>
```

We'll finish this part by fetching the data from our API.

```javascript
getProduct(){
    ...
    axios
        .get(`/api/v1/products/${category_slug}/${product_slug}`)
        .then(response => {
          this.product = response.data
        })
        .catch(error => {
          console.log(error)
        })
}
```

If we now go to the main page we can click on the `view details` button and show the detail page of each product.