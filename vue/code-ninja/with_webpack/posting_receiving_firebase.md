# posting_receiving_from_firebase

## Posting to Firebase

We go to [our Firebase console](https://console.firebase.google.com) and create a new project.
We then create a database and go to real-time database and copy the link.

In the addBlog.js file we create a method linked to the Submit button

```js
methods: {

    post: function(){
        const axios = require('axios');
        axios.post('https://netninja-vueblog.firebaseio.com/posts.json', this.blog)
            .then(data => {
                console.log(data);
                this.submitted = true
        })
    }

}
```

## Receiving from Firebase

*add to this ressource* later
