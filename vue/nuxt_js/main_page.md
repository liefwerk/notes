# The main page

We'll create a new folder in the `pages` folder called `jokes`.
Inside that folder we'll place an `index.vue` file with a default scaffold.

```vue
<template>
  <div>Jokes</div>
</template>

<script>
export default {};
</script>

<style></style>
```

## Creation of the header

In the components folder, let's create a `AppHeader.vue` file

```vue
<template>
  <header class="header">
    <h1 class="title">Dad Jokes</h1>
    <ul>
      <li>
        <nuxt-link to="/">Home</nuxt-link>
      </li>
      <li>
        <nuxt-link to="/jokes">Jokes</nuxt-link>
      </li>
      <li>
        <nuxt-link to="/about">About</nuxt-link>
      </li>
    </ul>
  </header>
</template>
```

and let's not forget to give it an export name.

```vue
<script>
export default {
  name: "Appheader",
};
</script>
```

Then, as in the normal VueJs framework, we'll import it in the general vue file.
This file is called `default.vue` and is located in the `layouts` folder

```vue
<script>
import AppHeader from "../components/AppHeader";

export default {
  components: {
    AppHeader,
  },
};
</script>
```

We'll also place it inside the `<template></template>` tags

```vue
<template>
  <div>
    <AppHeader />
    <nuxt />
  </div>
</template>
```
