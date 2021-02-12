# Dynamic values in templates

Another good thing about JSX is we can put dynamic values inside it.

## Creating a variable

`const title = "Welcome to the new blog"`

We then return the variable inside the JSX code: `<h1>{ title }</h1>`. This work for outputting variables but not objects.

We can also have dynamic values inside a `HTML tag`: `<a href={link}>Google site</a>`.