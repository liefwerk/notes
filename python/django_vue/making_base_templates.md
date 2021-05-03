# Making the base templates

## Modifying App.vue

We'll add a menu and the main pages. We'll first remove the content inside the `<style></style>` in the file called `src/App.vue`.

We then clean-up the content of the `<template></template>` tag and replace it with this:

```html
<div id="wrapper">
  <nav class="navbar is-dark">
    <div class="navbar-brand">
      <router-link to="/" class="navbar-item"><strong>Djackets</strong></router-link>

      <a class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbar-menu">
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
      </a>
    </div>

    <div class="navbar-menu" id="navbar-menu">
      <div class="navbar-end">
        <router-link to="/summer" class="navbar-item">Summer</router-link>
        <router-link to="/winter" class="navbar-item">Winter</router-link>

        <div class="navbar-item">
          <div class="buttons">
            <router-link to="log-in" class="button is-light">Log in</router-link>

            <router-link to="cart" class="button is-success">
              <span class="icon"><i class="fas fa-shopping-cart"></i></span>
              <span>Cart</span>
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </nav>

  <section class="section">
    <router-view/>
  </section>

  <footer class="footer">
    <p class="has-text-centered">Copyright (c) 2021</p>
  </footer>
</div>
```

## Modifying Home.vue

We can go to `src/views/home.vue` and replace the content with the following code:

```html
<template>
  <div class="home">
    Home
  </div>
</template>

<script>

export default {
  name: 'Home',
  components: {}
}
</script>
```

## Handling the burger menu with some JSX

If we click on the burger menu from a phone, nothing happens. This is because the handling has to be written in `JSX` in our `App.vue` file.

We create a `boolean` variable that we'll use to activate and deactivate our burger menu.

```javascript
<script>
export default {
  data() {
    return {
      showMobileMenu: false,
    }
  }
}
</script>
```

Then we add a `@click` event on our menu link: 

```html
<a class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbar-menu" @click="showMobileMenu = !showMobileMenu">
...
```

And finally we bind this event on a class for the rest of the menu:

```html
<div class="navbar-menu" id="navbar-menu" v-bind:class="{ 'is-active': showMobileMenu }">
...
```