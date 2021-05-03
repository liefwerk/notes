# View the cart

Create a new file called `Cart.vue`. Set up the template and script parts. Import the view to the router file.

```html
<template>
  <div class="page-cart">
    <div class="columns is-multiline">
      <div class="column is-12">
        <h1 class="title">Cart</h1>
      </div>

      <div class="column is-12 box">
        <table>
          <thead>
            <tr>
              <th>Product</th>
              <th>Price</th>
              <th>Quantity</th>
              <th>Total</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <CartItem 
              v-for="item in cart.items"
              :key="item.product.id"
              :initialItem="item"
            />
          </tbody>
        </table>
        <p>You don't have any product in your cart...</p>
      </div>
    </div>
  </div>
</template>
```

```javascript
<script>
import axios from 'axios'
import CartItem from '@/components/CartItem.vue'

export default {
  name: 'Cart',
  components: {
    CartItem
  }
  data (){
    return {
      cart: {
        items: []
      }
    }
  }
}
</script>
```

## Creating the Cart Item component

Create a new file called `CartItem.vue` in the components folder.

```html
<template>
  <tr>
    <td><router-link :to="item.product.get_absolute_url">{{ item.product.name }}</router-link></td>
    <td>${{ item.product.price }}</td>
    <td>
      {{ item.quantity }}
    </td>
    <td>${{ getItemTotal(item).toFixed(2) }}</td>
    <td><button class="delete"></button></td>
  </tr>
</template>
```

```javascript
<script>
export default {
  name: 'Cartitem',
  props: {
    initialItem: Object
  },
  data() {
    return {
      item: this.initialItem
    }
  },
  methods: {
    getItemTotal(item){
      return item.quantity * item.product.price
    }
  }
}
</script>
```

## Summary of the cart's content

Go back to `Cart.vue` to add some computed functions.

```javascript
computed: {
    cartTotalLength() {
        return this.cart.items.reduce((acc, curVal) => {
            return acc += curVal.quantity
        }, 0)
    },
    cartTotalPrice() {
        return this.cart.items.reduce((acc, curVal) => {
            return acc += curVal.product.price * curVal.quantity
        }, 0)
    },
}
```

Then in the template, below the `v-for/v-else` add the following `HTML`.

```html
<div class="column is-12 box">
    <h2 class="subtitle">Summary</h2>

    <strong>${{ cartTotalPrice.toFixed(2) }}</strong>, {{ cartTotalLength }} items

    <hr>

    <router-link to="/cart/checkout" class="button is-dark">Proceed to checkout</router-link>
</div>
```

## Interacting with the cart items

Go to the `CartItem.vue` file and add the following methods.

```javascript
methods: {
    getItemTotal(item) {
        return item.quantity * item.product.price
    },
    decrementQuantity(item) {
        item.quantity -= 1
        if (item.quantity === 0) {
            this.$emit('removeFromCart', item)
        }
        this.updateCart()
    },
    incrementQuantity(item) {
        item.quantity += 1
        this.updateCart()
    },
    updateCart() {
        localStorage.setItem('cart', JSON.stringify(this.$store.state.cart))
    },
    removeFromCart(item) {
        this.$emit('removeFromCart', item)
        this.updateCart()
    },
},
```

These methods will be accessible on each item.

```html
<tr>
    ...
    <a @click="decrementQuantity(item)">-</a>
    <a @click="incrementQuantity(item)">+</a>
    ...
    <td><button class="delete" @click="removeFromCart(item)"></button></td>
</tr>
```

Currently, if we remove an item from the cart, it doesn't do any thing. The reason is that it emits `removeFromCart` but there isn't a function that catches it. Go to `Cart.vue` and inside the `<CartItem />` tag, add `v-on:removeFromCart="removeFromCart" />`.

In `Cart.vue` create a new method called `removeFromCart`.

```javascript
methods: {
    removeFromCart(item) {
        // this filters the current item from the cart item array
        this.cart.items = this.cart.items.filter(i => i.product.id !== item.product.id)
    }
},
```