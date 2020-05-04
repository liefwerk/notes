# Intro and Setup Introduction

Cloud functions are function runned by the server on firebase. It can be a way to run functions without using a user account inside the app.
Firstly, we'll install `firebase-tools`

`npm i -g firebase-tools`

We then run the command firebase login, firebase init & firebase deploy

## Create a function

To create a function, we'll go to the new folder functions/index.js

```
exports.helloWorld = functions.https.onRequest((request, response) => {
    response.send("Hello, Ninjas");
});
```

Then in the terminal we'll deploy the functions folder only

`firebase deploy --only functions`