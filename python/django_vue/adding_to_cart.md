# Adding to cart logic

## Add functionality to VueX

This adding to cart logic will operate inside our vue store `VueX`. Let's go to the `mutations` function. We'll also use `localStorage`.

```javascript
mutations: {
    // this function initialises the cart
    initializeStore(state) {
      // checks if the cart exists
      if (localStorage.getItem('cart')) {
        // in this case it will parse and store in inside our store variable named cart
        state.cart = JSON.parse(localStorage.getItem('cart'))
      } else {
        // otherwise it creates it
        localStorage.setItem('cart', JSON.stringify(state.cart))
      }
    },
    // this function adds the selected item to cart
    addToCart(state, item) {
      // first is checks if the item is already in the cart
      const exists = state.cart.items.filter(i => i.product.id === item.product.id)
      // if it is, it will add the selected quantity to the current product in the cart
      if (exists.length) {
        exists[0].quantity = parseInt(exists[0].quantity + parseInt(item.quantity))
      } else {
        // otherwise it will simply push the new item to the cart
        state.cart.items.push(item)
      }
      
      // now it stores the cart inside the localStorage
      localStorage.setItem('cart', JSON.stringify(state.cart))
    }
  },
```

## Initialize store in App.vue

In `App.vue` let's add a few lines to our `<script></script>` tag.

```javascript
export default {
  data() {
    return {
      showMobileMenu: false,
      // here we mimic the store structure for the cart to access it later
      cart: {
        items: []
      }
    }
  },
  beforeCreate(){
    // commit is used to call the mutations we setup in the VueX store
    this.$store.commit('initializeStore')
  }
}
```

Now we want to show the number of items currently inside the cart. In the same file `App.vue` let's use another hook called `computed`.

```javascript
  // computed values are calculated on things around the whole page
  computed: {
    // this function will calculate the quantity of products inside the cart
    cartTotalLength(){
      // we initialize the length
      let totalLength = 0
      
      // for each item in the cart...
      for (let i=0; i < this.cart.items.length; i++){
        // we add 1 for each quantity
        totalLength += this.cart.items[i].quantity
      }
      // then we return the total quantity
      return totalLength
    }
  }
```

## Link the add to cart button to the function

Next step is to actually call the `addToCart()` function when we click on the `Add to cart button`. Let's open the `Product.vue` file. After the function `getProduct()` in the `method` hook in  `product.vue`, well add the new function `addToCart()`.

```javascript
methods: {

    getProduct(){
        ...
    },
    addToCart(){
      if (isNaN(this.quantity) || this.quantity < 1){
        this.quantity = 1
      }

      const item = {
        product: this.product,
        quantity: this.quantity
      }

      this.$store.commit('addToCart', item)
    }
}
```

We'll also link that function to the button. in the same file, add the following `HTML` code.

```html
<template>
    <div class="field has-addons mt-6">
        ...
        <div class="control">
            <a class="button is-dark" @click="addToCart">Add to cart</a>
        </div>
    </div>
</template>
```

The last step is to populate our `cart` function of the main `App.vue` with the data of the VueX cart.

```javascript
mounted() {
    this.cart = this.$store.state.cart
},
```

## Adding a toast for the action

A toast is a message sent when an action is performed. It generally has a message telling the action has been successful.

First, we'll install a package called `bulma-toast`: `yarn add bulma-toast`. Then we import it in the `Product.vue` file: `import { Toast } from 'bulma-toast'`.

Then at the end of our `addToCart()` function we add a new `Toast()`.

```javascript
addToCart(){
    ...
    this.$store.commit('addToCart', item)

    Toast({
        message: 'The product was added to the cart',
        type: 'is-success',
        dismissible: true,
        pauseOnHover: true,
        duration: 2000,
        position: 'bottom-right',
    })
}
```