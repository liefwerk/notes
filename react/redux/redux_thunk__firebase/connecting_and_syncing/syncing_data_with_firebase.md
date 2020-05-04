# Syncing Data with Firebase

To sync up our redux state with the firebase database.
First, in our Root reducer we'll import the package `firestoreReducer` from `redux-firestore`

```

import { firestoreReducer } from 'redux-firestore'

This is an already made reducer that will know about our projects and how to access the data (it receives the access from the config)
The second step is to connect the firestore reducer to a component.
```

We import `compose()` and `firestoreConnect()`

```
import { firestoreConnect } from 'react-redux-firebase'
import { compose } from 'redux'
```


and when exporting the component, include the `firestoreConnect()` function as an Higher Order Component with the `connect()` function

```
export default compose(

    connect(mapStateToProps),
    firestoreConnect([
    { collection: 'projects'}
    ])

)(Dashboard)
```

We then return the data from firestore inside the `mapStateToProps()` function

```
return {

    projects: state.firestore.ordered.projects

}
```

