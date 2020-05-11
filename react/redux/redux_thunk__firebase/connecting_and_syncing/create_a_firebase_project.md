# Create a Firebase Project

First of all let's create a firebase project with our google account.

Once the project is created, we install firebase using npm

`npm i firebase`

Then we copy the JS configuration from our firebase account

```js
import firebase from 'firebase/app'
import 'firebase/firestore'
import 'firebase/auth'

// Your web app's Firebase configuration
var firebaseConfig = {

    apiKey: "AIzaSyBya6TKbNEk7LRqldLSxYcK8Th-dG2JI6k",
    authDomain: "netninja-marioplan-a75c3.firebaseapp.com",
    databaseURL: "https://netninja-marioplan-a75c3.firebaseio.com",
    projectId: "netninja-marioplan-a75c3",
    storageBucket: "netninja-marioplan-a75c3.appspot.com",
    messagingSenderId: "142456329399",
    appId: "1:142456329399:web:8186d81ecb6a9e1681e932"

};

// Initialize Firebase
firebase.initializeApp(firebaseConfig);
firebase.firestore().settings({ timestampsInSnapshots: true})

export default firebase
```
