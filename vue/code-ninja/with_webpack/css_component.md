# component_css

If we use the `<style>` tag in the .vue files, it puts it on the head of the DOM, which applies it to every component.

We can add scoped to the `<style>` tag to make it local.

```css
<style scoped>
h1 {

color: green;

}
</style>
```
