# Lifecycle Methods

We have a **Mounting**, **Updating** and **Unmounting** phase.

**Mounting**

When it is first created and mounted.

First method is `constructor()`.

Second method is `getDerivedStateFromProps()`.
It enables component to update it's internal state as the result of changes in the props. It triggers on first render and whenever we recieve updated props.
Possible to compare the props and the state.

Then `render()`.
Only required method in the component, will return some form of JSX.

Then we get `ComponentDidMount()`
Fires once component is mounted - good to get exterior data like from a database.

**Updating**

First method is `getDerivedStateFromProps()`

Then `ShouldComponentUpdate()`
It gets the current and new states / props. We can return false to prevent the component to render.
Only returns true when there is a change.

Then `render()`

After that, we have `GetSnapshotBeforeUpdate()`, we get read access to the DOM before the change is commited to it.
We get values such as the window position, and return it inside the method. Method value is passed through the last hook.

Then `ComponentDidUpdate()` that is called after template is rendered. Good place to get external data.
If we update state inside this hook, we could get an inifite loop.

*Examples*

**componentDidMount**

```
componentDidMount(){
    console.log('componentmounted');
}
```

**componentDidUpdate**

```
componentDidUpdate(prevProps,prevState){
    console.log("componentupdated");
    console.log(prevProps,prevState);
}
```