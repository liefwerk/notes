# Stateless Components

Differents types of components:

Container components:

* not concerned with UI or look
* contain state
* serve as data sources
* contain lifecycle hooks
* use classes to create them

UI Component:

* don't contain states
* receive data from props
* only concerned with UI
* use functions to create, not classes

## Example

```js
const Ninjas = (props) => {
    const { ninjas } = props;
}
```

It also is possible to do it the destructuring way:

```js
const Ninjas = ({ninjas}) => {

}
```

It saves a few lines.
