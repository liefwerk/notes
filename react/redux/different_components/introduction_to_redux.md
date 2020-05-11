# Introduction to Redux

Redux is a central data store that shares data between components.
If we want data, we reach out from the components to the central data store.

There is a process whe we want to alter the data.

We define a central store, where the data ill be kept.
When we want to access, component siubscribes to changes, redux apasses the data in the form of props.

Changing data is a process, makes it easier to debug.

We decide to change, we dispatch the action. (eg. add post, add name..)
We can pass a payload (data that we pass along), the data we want to add.

Then the action is passed as a reducer. It looks at the action, takes the data that we need and updates it in the store.
