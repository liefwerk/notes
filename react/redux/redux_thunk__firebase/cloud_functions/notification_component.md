# Notification System

First we'll create a function that reacts to a new project being created and one that will react to a new user joining.
In index.js in the functions folder we import `firebase-admin`

`const admin = require('firebase-admin');`

then we initialize the app with the config

`admin.initializeApp(functions.config().firebase);`

and we create/export the cloud function

```js
exports.projectCreated = functions.firestore

.document('projects/{projectId}')
.onCreate(doc => {

const project = doc.data();
const notification = {
    content: 'Added a new project',
    user: \`${project.authorFirstName} ${project.authorLastName}\`,
    time: admin.firestore.FieldValue.serverTimestamp()
}
return createNotification(notification)

})
```

That function needs to return a notification, to do that we'll first create a `createNotification()` function

```js
const createNotification = (notification => {

return admmin.firestore().collection('notifications')
.add(notification)
.then(doc => console.log('notification added', doc));

});
```

We then write firebase deploy in the console to deploy the cloud function

`firebase deploy --only functions`
