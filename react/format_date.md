# Format Dates

## How to format Dates with Moment.js

We'll use Moment.js to format the date, first let's install it with `npm`

```js
npm i moment
```

Then we import it inside the right component

`import moment from 'moment'`

Then where we output the date inside the JSX or HTML, we surround the `toDate()` with the `moment()` method.
We can also add another method to structure the date, in this example we'll use `calendar()`

More examples in the [Moment.js reference file](https://momentjs.com/)

`<p className="grey-text">{moment(project.createdAt.toDate()).calendar()}</p>`
