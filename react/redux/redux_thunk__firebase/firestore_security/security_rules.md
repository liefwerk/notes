# Security Rules in Firestore

## Security Rules

There are a way to hide our data, documents from others.

To access the Rules in the Firebase Console, we go to the Database tab and Rules.
The way we declare rules is to match certain paths and declare rules for these paths (a bit like linux).

`service cloud.firestore {}` stores rules for the firestore only.

`match /databases/{database}/documents {}` means that rule should reach any firestore database in our project

`match /{document=**}{}` is saying match any documents in the database

and the rules applied say this:

`allow read, write: if request.time < timestamp.date(2020, 5, 27);`

which allow anyone to rad and write our documents. Once we go into production, we have to update them.

Here are the rules that we'll add

```js
match /projects/{project} {

    allow read, write: if request.auth.uid != null

}

match /users/{userId} {

    allow create
    allow read: if request.auth.uid != null
    allow write: if request.auth.uid == userId

}
```
