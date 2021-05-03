# View a category

## Create a new api view-set for the categories

Go to `views.py`. First let's add a new fonction called `CategorySerializer` at the top.

```python
from .models import Product, Category
from .serializer import ProductSerializer, CategorySerializer
```

Then below the `ProductDetail` class, we add the following code.

```python
# the nw view-set is as follows
class CategoryDetail(APIView):
  def get_object(self, category_slug):
    try:
      return Category.objects.get(slug=category_slug)
    except Category.DoesNotExist:
      raise Http404

  def get(self, request, category_slug, format=None):
    category = self.get_object(category_slug)
    # we'll create a new serializer in the next step
    serializer = CategorySerializer(category)
    return Response(serializer.data)
```

## Create the categories serializer

In `serializer.py` let's add the new `CategorySerializer` class.

```python
class CategorySerializer(serializers.ModelSerializer):
  products = ProductSerializer(many=True)
  class Meta:
    model = Category
    fields = (
      "id",
      "name",
      "get_absolute_url",
      "products"
    )
```

Now let's add a new path to the product's `urlpatterns` list.

```python
urlpatterns = [
  ...
  path('products/<slug:category_slug>/', views.CategoryDetail.as_view()),
]
```

## Showing the category on the front end
### Adding a new view

Go to the vue folder and inside the `views` folder create a new file called `Category.vue`.

Here's the template part.

```html
<template>
  <div class="page-category">
    <div class="columns is-multiline">
        <div class="column is-12">
            <h2 class="is-size-2 has-text-centered">{{ category.name }}</h2>
        </div>
    </div>
  </div>
</template>
```

Here's the `script` part.

```javascript
<script>
// the imports
import axios from 'axios'
import { toast } from 'bulma-toast'

export default {
  name: 'Category',
  // our variables
  data() {
    return {
      category: {
        products: []
      }
    }
  },
  // calling the fecthing function when the component is mounted
  mounted() {
    this.getCategory()
  },
  methods: {
    // the fetching function with async/await
    async getCategory() {
    // the slug is inside the route we set up in the API, we can get it from
    // the $route parameters
      const categorySlug = this.$route.params.category_slug
      // this is for the loading bar
      this.$store.commit('setIsLoading', true)

      await axios
        .get(`/api/v1/products/${categorySlug}/`)
        .then(reponse => {
          this.category = response.data
          // changing the document title to the name of the category we get from the api
          document.title = this.category.name + ' | Djackets'
        })
        .catch(error => {
          console.log(error)
          // let's throw a toast when something seems fishy
          toast({
            message: 'Someting went wrong. Please try again.',
            type: 'is-danger',
            dismissible: true,
            pauseOnHover: true,
            duration: 2000,
            position: 'bottom-right',
          })
        })
      // deactivation of the loading bar
      this.$store.commit('setIsLoading', false)
    }
  }
}
</script>
```

### Adding the view to the router

In the `router/index.js` file, let's import our new component: `import Category from'../views/Category.vue'`. Now that the category is imported, add it below the existing routes.

```javascript
const routes = [
  ...
  {
    path: '/:category_slug',
    name: 'Category',
    component: Category
  },
]
```

The piece of code used for showing the products in cards could be reused to show the products of each category. Because it is a reusable piece of code, we should make a component out of it.

## Conversion to component

The piece of code is the following.

```html
<div class="column is-3">
    <div class="box">
        <figure class="image mb-4">
            <img :src="product.get_thumbnail">
        </figure>

        <h3 class="is-size-4">{{ product.name }}</h3>
        <p class="is-size-6 has-text-grey">${{product.price}}</p>

        <router-link 
            :to="product.get_absolute_url" 
            class="button is-dark mt-4"
        >
            View details
        </router-link>
    </div>
</div>
```

Inside the `/components/` folder let's create a new `ProductBox.vue` file. The content of the `template` tag is as follows. The only difference is that the v-for has been removed.

```html
<template>
    <div class="column is-3">
        <div class="box">
          <figure class="image mb-4">
            <img :src="product.get_thumbnail">
          </figure>

          <h3 class="is-size-4">{{ product.name }}</h3>
          <p class="is-size-6 has-text-grey">${{product.price}}</p>

          <router-link :to="product.get_absolute_url" class="button is-dark mt-4">View details</router-link>
        </div>
      </div>
</template>
```

Then the `script` tag contains the name and what the `props` will contain.

```javascript
<script>
export default {
  name: 'ProductBox',
  props: {
    product: Object
  }
}
</script>
```

Go to `Home.vue`, remove the content inside the `style` tag at the bottom and paste it at the bottom of the `ProductBox.vue` file.

```css
<style scoped>
.image {
  margin: -1.25rem -1.25rem 0 -1.25rem;
}
</style>
```

Then, still in `Home.vue`, let's import the `ProductBox` component with the following import statement.

`importProductBox from '@/components/ProductBox'`

Next is to include it inside the components of the view.

```javascript
components: {
    ProductBox
},
```

And lastly, include the component in the `template`. Notice that the `v-for` is included inside the `<ProductBox>` element so it gets generated for each product fetched from the API.

```html
<ProductBox
    v-for="product in latestProducts"
    :key="product.id"
    :product="product"
/>
```

TODO
- add explanation for category
- add explanation for watch $route 