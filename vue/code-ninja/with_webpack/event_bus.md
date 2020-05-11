# events

To create an event:

`this.$emit('changeTitle', 'Vue Wizards');`

Then we can listen to this event in the parent component.

```md
<custom-tag @changeTitle="updateTitle($event)"></custom-tag>

methods: {
    updateTitle: (updatedTitle) => {
        this.title = updatedTitle
    }
}
```

## Event Bus

The event bus is a way of sharing the change of data between the components without going back to the parent component.

To create an event bus (in the main.js):

```js
export const bus = new Vue();

// then we import it inside the components
import { bus } from '../main'
```

To emit en event:

```js
methods: {
    changeTitle: () => {
        bus.$emit{'titleChanged', 'New title'}
    }
}
```

To receive the event, inside the export default:

```js
created(){
    bus.$on('titleChanged', (data) => {
        this.title = data;
    })
}
```
