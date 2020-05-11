# slots

## What are slots in VueJS

We've seen that we can pass data, but how can we pass an HTML template into the child component?
We can do it using slots.

First, in the html tag we define what we want to pass down.
In the parent component, we add some HTML tags inside the custom tag.

```html
<h2>I am the slot title</h2>
<p>Paragraph</p>
```

Then inside the children template we add the `<slot></slot>` tag

```html
<template>
    <div>
        <h1>I am a Form Helper</h1>
        <slot></slot>
    </div>
</template>
```

We can also name the slots in the parent file

```html
<h2 slot="title">I am the slot title</h2>
<p slot="paragraph">Paragraph</p>
```

and name the slots accordingly in the component

```html
<slot name="title"></slot>
    <h1>I am a Form Helper</h1>
<slot name="paragraph"></slot>
```
