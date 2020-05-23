# Displaying the jokes

To display the jokes, we'll create a specific component called `Joke.vue`

```vue
<template>
  <div class="joke">
    <p>{{ joke }}</p>
  </div>
</template>

<script>
export default {
  name: "Joke",
  props: ["joke", "id"],
};
</script>

<style>
.joke {
  padding: 1rem;
  border: 1px dotted #ccc;
  margin: 1rem 0;
}
</style>
```

## Looping through the array

We'll display all the jokes with a `v-for` attribute in our `jokes/index.vue` file.
We import the Joke component, construct the v-for loop and pass the props inside our `<Joke />` tag.

```vue
<template>
  <div>
    <Joke
      v-for="joke in jokes"
      :key="joke.id"
      :id="joke.id"
      :joke="joke.joke"
    />
  </div>
</template>

<script>
import axios from "axios";
import Joke from "../../components/Joke";

export default {
  components: {
    Joke,
  },
};
</script>
```
