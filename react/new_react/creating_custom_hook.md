# Creating a custom Hook

Having written all the logic inside the `useEffect` Hook, if we want to use it again in another `Component`, we need to write it again. That isn't efficient or easy to manage. We could export this logic to another javascript file. By doing this we create a custom hook.

Inside the `src` folder we'll create `useFetch.js`.

```
import { useState, useEffect } from 'react';

const useFetch = (url) => {
    const [data, setData] = useState(null);
    const [isPending, setIsPending] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
        setTimeout(() => {
            fetch(url)
            .then(res=> {
                if (!res.ok) {
                    throwError('could not fetch the data for that ressource.');
                }
                return res.json();
            })
            .then(data=> {
                setData(data);
                setIsPending(false);
                setError(null);
            })
            .catch(err=> {
                setError(err.message);
                setIsPending(false);
            })
        }, 1000);
    }, []);
    return { data, isPending, error }
}

export default useFetch;
```

Then, inside our `Home` component we'll import the `useFetch` custom hook: `importuseFetchfrom'./useFetch';` and put it inside our component with some data destructuring: `const { data: blogs, isPending, error } = useFetch('http://localhost:8000/blogs');`.