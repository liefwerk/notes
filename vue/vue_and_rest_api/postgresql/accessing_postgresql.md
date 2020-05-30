# Accessing Postgresql

We'll assume that postgresql is already installed and you have a username to access it.
Let's access the postgresql terminal with the `psql` command.

```bash
sudo -i -u postgres
psql
```

## Creating the database

While you are connected with the postgres user, we'll create our first database.

```sql
CREATE DATABASE firstapi;
# This command will show all our databases
\l
```

## Connect to the database

```sql
\c firstapi;
CREATE TABLE users(
  id SERIAL PRIMARY KEY,
  name VARCHAR(40),
  email TEXT
);
\dt
INSERT INTO users (name, email) VALUES
('joe', 'joe@imb.com'),
('ryan', 'ryan@fastweb.com');
SELECT * FROM users;
```

## Initiate the pg package

Before accessing our database with `pg`, let's lay the ground code in the `index.controllers.js` file

```js
const { Pool } = require("pg");

const pool = new Pool({
  host: "45.33.98.225",
  user: "postgres",
  password: "",
  database: "firstapi",
  post: "5432",
});
```

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

### Handling postgresql errors

In this case, I have a postgresql installed on my own VPS machine.
When I try to reach it, I get a ECONNREFUSED error.

In the terminal of the machine where Postgresql is installed, let's edit the conf file.
In this case it is situated in `/etc/postgresql/12/main/postgresql.conf`

In the line listen_address = `'localhost'` we'll replace localhost with `'*'`.

Then in the `/etc/postgresql/12/main/pg_hba.conf` file we'll add this at the end of the file:

```conf
host    all             all              0.0.0.0/0                       md5
host    all             all              ::/0                            md5
```

And since I have a firewall, let's add a rule to ufw

```bash
sudo ufw allow from any to any port 5432 proto tcp
```

#### Using another user

If you want to use another user (not postgres, alias the superuser), you need to GRANT ACCESS to the tables of the database.

```sql
GRANT ALL PRIVILEGES ON TABLE your_table TO username;
GRANT USAGE, SELECT ON SEQUENCE your_table_seq TO username;
```
