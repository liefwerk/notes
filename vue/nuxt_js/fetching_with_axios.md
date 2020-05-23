# Fetching from an API

To fetch our data, we'll use axios.

In our `jokes/index.vue`, wet's add this bit of code

```vue
<script>
import axios from "axios";

export default {
  data() {
    return {
      jokes: [],
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json",
      },
    };
    try {
      const res = await axios.get("https://icanhazdadjoke.com/search", config);
      this.jokes = res.data.results;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
```
