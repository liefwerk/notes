# useEffect cleanup

While the fetch is going, if we change the page it will get an error. This happens because we can't perform a change of state in a component that doesn't share this state.

## Using abortController

We start by going to our `useFetch` component and create a new `abortController`: `const abortCont = new AbortController();`. We then pass it inside the fetch this way: `fetch(url, { signal: abortCont.signal })`.

Finally we can abort the fetch by returning a function after the fetching: `return () => abortCont.abort();`.

inside the catch function we can also stop the state from being changed:

```javascript
.catch(err=> {
    if (err.name==='AbortError') {
        console.log('fetch aborted');
    } else {
        setError(err.message);
        setIsPending(false);
    }
})
```