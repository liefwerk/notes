# First page

Let's create a new file in the `page` folder.
That new file is called `about.vue` and we'll write a simple h1 and p tag inside

```vue
<template>
  <div>
    <h1>About DadJokes</h1>
    <p>This is an app that displays corny dad jokes.</p>
  </div>
</template>
```

Only by creating that file, it creates the routing by itself.

## Handling SEO

To handle SEO, we can create a `head()` function and associate a title and meta tag.

```vue
<script>
export default {
  head() {
    return {
      title: "About The DadJoke App",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Best place for corny dad jokes!",
        },
      ],
    };
  },
};
</script>
```
