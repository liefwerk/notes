# Creating a search component for the jokes

Let's create a file called `SearchJokes.vue` in our `components` folder.
Inside we'll place this bit of code

```vue
<template>
  <form @submit.prevent="onSubmit">
    <label for="search">Search</label>
    <!-- in this input we use v-model to associate it's content with the text variable -->
    <input placeholder="other side dad joke" type="text" v-model="text" />
  </form>
</template>

<script>
export default {
  name: "SearchJokes",
  data() {
    return {
      // here we return the text from the input field
      text: "",
    };
  },
  methods: {
    // this function sends our text through an emit called earch-text
    onSubmit() {
      this.$emit("search-text", this.text);
      this.text = "";
    },
  },
};
</script>
```

Now in the `index.vue` of our `jokes` folder, let's import this component

```vue
<script>
import SearchJokes from "../../components/SearchJokes";

export default {
  components: {
    Joke,
    SearchJokes
</script>
},
```

and in the template we'll pass that component as a tag

```vue
<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    ...
  </div>
</template>
```

We'll also add a method called `searchText`.

```vue
<script>
methods: {
  // the method takes the text sent through the emit
  async searchText(text) {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      // we'll pass that text variable in the fetching url of the api
      const res = await axios.get(
        `https://icanhazdadjoke.com/search?term=${text}`,
        config
      );
      // we add the result to our jokes array
      this.jokes = res.data.results;
    } catch (error) {
      console.log(error);
    }
  }
},
</script>
```

That's it, our app is finished.
We could add some more styling to make it slicker.
