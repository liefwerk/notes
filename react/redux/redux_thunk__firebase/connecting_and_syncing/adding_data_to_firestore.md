# Adding Data to Firestore

In order to add data to firestore, we'll first initialize the `getFirestore()` function

`const firestore = getFirestore();`

That gives us a reference to the Firestore database.

`firestore.collection('projects')`

To add a new document we do this

```
firestore.collection('projects').add({

    ...project,
    authorFirstName: 'Net',
    authorListName: 'Ninja',
    authorId: 12345,
    createdAt: new Date()
    
})
```

All this data is going to our Firestore and be added as a new document inside our collection.
That will also generate a new document id.

Because it's going to take some time to do, it'ss take a promise (asynchronous method).
We can use .then() and a callback function

```
firestore.collection('projects').add({

    ...project,
    authorFirstName: 'Net',
    authorListName: 'Ninja',
    authorId: 12345,
    createdAt: new Date()
    
}).then(() => {

    dispatch({ type: 'CREATE_PROJECT', project })
    
}).catch((err) => {

    dispatch({ type: 'CREATE_PROJECT_ERROR', err})
    
})
```

In our projectReducer.js we can add these next actions to our switch function

```
const projectReducer = (state = initState, action) => {

    switch (action.type){
    case 'CREATE_PROJECT':
        return state;
    case 'CREATE_PROJECT_ERROR':
        console.log('create project error', action.err);
        return state;
    default:
        return state;
    }

}
```
