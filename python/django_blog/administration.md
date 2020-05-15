# Administration

As we saw before, there already is an admin part on our application.
In order to access it, we'll have to create an admin user.

But first, let's create a table to store it in the database.
We'll do the first migration to create those tables.

`python3 manage.py makemigrations`

then

`python3 manage.py migrate`

Since our database has been migrated, we can create our super user.

`python3 manage.py createsuperuser`

We can now access the admin page, create users and manage it.
