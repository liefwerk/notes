# Using Thunk

First, let's install `redux-thunk`

`npm i redux-thunk`

Then in the index.js file we import `Thunk`

`import thunk from 'redux-thunk'`

And we also import the method `applyMiddleware` from redux, which will help us to setup `Thunk`

`import { createStore, applyMiddleware } from 'redux'`

The next step is to setup thunk inside that last imported method `applyMiddleware()`

`const store = createStore(rootReducer, applyMiddleware(thunk));`

## First project action

To initiate our first project action, we'll export a function that takes the project as a parameter.
That function will return another function that takes the dispatch and the state as parameters.

Inside the dispatch function, we'll create the object with it's type and it's content.export const createProject = (project) => {

```
return (dispatch, getState) => {
    // make async call to database
    dispatch({ type: 'CREATE_PROJECT', project })
}
```

Once the `createProject` function is created, we import it in the components that will be allowed to modify the state.
We'll be using the `mapDispatchToProps` function, it is constructed as follows:

```
const mapDispatchToProps = (dispatch) => {
return {

// it returns a createProject function that tales the project as a parameter, then uses the dispatch method to send the imported function with the project as a parameter

 createProject: (project) => dispatch(createProject(project))
}
}// we pass null as the first parameter because we do not have a mapStateToProps() function to call
export default connect(null, mapDispatchToProps)(CreateProject)
```

To call the function, we load it from the state

```
this.props.createProject(this.state)
```

Then, that action is receives by a reducer and will return the state depending of the action type.

```
const projectReducer = (state = initState, action) => {

    switch (action.type){
    case 'CREATE_PROJECT':
        console.log('project created', action.project);
    }
    
    return state

}
```