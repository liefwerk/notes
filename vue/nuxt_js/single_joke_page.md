# Single Joke page

To show a single joke, we have to handle the id parameter inside the url.

With Nuxt JS, we'll create another fodler inside our `jokes`folder called `_id`
Then inside we'll create a `index.vue` file.

```vue
<!-- the template view -->
<template>
  <div class="">
    <nuxt-link to="/jokes">Back to the Jokes</nuxt-link>
    <h2>
      {{ this.joke.joke }}
    </h2>
    <hr />
    <small>Joke ID: {{ $route.params.id }}</small>
  </div>
</template>
```

```vue
<script>
// the script with the axios fetching
import axios from "axios";
export default {
  data() {
    return {
      joke: {},
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json",
      },
    };
    try {
      // this time we'll only fecth an unique id taken from the url parameter
      const res = await axios.get(
        `https://icanhazdadjoke.com/j/${this.$route.params.id}`,
        config
      );
      this.joke = res.data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
```

To access that view, we'll wrap each joke div inside a `nuxt-link` tag.

```html
<nuxt-link :to="'jokes/' + id">
  <div class="joke">
    <p>{{ joke }}</p>
  </div>
</nuxt-link>
```
