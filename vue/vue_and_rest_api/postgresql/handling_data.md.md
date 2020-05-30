# Handling the data

## Printing the response in JSON format

Now that we get our data from the request, let's print it to our website.

```js
const getUsers = async (req, res) => {
  try {
    const response = await pool.query("SELECT * FROM users");
    res.status(200).json(response.rows);
  } catch (error) {
    console.log(error);
  }
};
```

## Create a user

To handle the creation of a user, we'll create another route.

```js
router.post("/users", createUser);
```

```js
const createUser = async (req, res) => {
  try {
    const { name, email } = req.body;
    const response = await pool.query(
      "INSERT INTO users (name, email) VALUES ($1, $2)",
      [name, email]
    );
    console.log(response);
    res.send("user created");
  } catch (error) {
    console.log(error);
  }
};
```

Now when we sent a post request through the /users endpoint, we receive this message:

```bash
Result {
  command: 'INSERT',
  rowCount: 1,
  oid: 0,
  rows: [],
  fields: [],
  _parsers: undefined,
  _types: TypeOverrides {
    _types: {
      getTypeParser: [Function: getTypeParser],
      setTypeParser: [Function: setTypeParser],
      arrayParser: [Object],
      builtins: [Object]
    },
    text: {},
    binary: {}
  },
  RowCtor: null,
  rowAsArray: false
}
```
