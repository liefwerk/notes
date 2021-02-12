# Redirecting the user

We can use a hook called `useHistory`. Inside the Create component we want to import this hook.

`import { useHistory } from 'react-router-dom'`.

We then declare it in a variable: `const history = useHistory();`. There are several methods so we can go back or further into history.

To go back we write the method `go`: `history.go(-1);`.
To redirect the user to a url we use the `push` method: `history.push('/')`.