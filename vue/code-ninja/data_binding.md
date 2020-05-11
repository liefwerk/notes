# data_binding

We've seen how to output data from an instance.
We can bind properties to any HTML tag with v-bind:

```
new Vue({

// targets <div class="" id="vue-app"></div>
el: '#vue-app',
data: {
    website: 'https://website.com'
}

});

<a v-bind:href="website">The Net Ninja</a>
```

There is a shorthand called :

`<a :href="website">The Net Ninja</a>`

If we want to output HTML code from our JS scripts, we can use `v-html=""`

`<p v-html="websiteTag"></p>`