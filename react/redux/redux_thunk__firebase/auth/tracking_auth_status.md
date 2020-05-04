# Tracking Auth Status

In Navbar.js we'll pass the props and use a turnary operator to show the appropriated links

```
const { auth } = props
const links = auth.uid ? <SignedInLinks /> : <SignedOutLinks />
```

Then in the JSX we output the constant links

`{ links }`

That's it !