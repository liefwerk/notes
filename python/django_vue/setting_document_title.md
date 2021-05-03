# Setting the document title

If we look at our website, right now each page has the name of the app as the page title. Let's see how we can modify our titles dynamically.

## Handling dynamic titles

For each view, we'll add a `document.title`. First let's modify our `Product.vue` file. In the `getProduct()` method we have access to the product's name, let's use that to update the title.

Add `document.title = this.product.name + ' | Djackets'` just after we assign `response.data` to our `product` array.

Then in `Home.vue`, inside the `mounted()` hook let's add `document.title = 'Home | Djackets'`