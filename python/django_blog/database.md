# Working with databases

## Creating a table

Let's create our own tables.

Django have it's own ORM (Object Relational Mapper).
You can use different databases without changing the code.
That makes it easier when migrating to production.

Within our blog app, django generated a `models.py` file.
Let's add some code to set it up.

```py
from django.db import models
# we import a timezone method to post the date
from django.utils import timezone
# we import the user model from django
from django.contrib.auth.models import User

# we create a new Post model
class Post(models.Model):
  title = models.CharField(max_length=100)
  content = models.TextField()
  date_posted = models.DateTimeField(default=timezone.now)
  author = models.ForeignKey(User, on_delete=models.CASCADE)
```

Once we updated the models.py file, we can confirm it with the command line.

`python3 manage.py makemigrations`

That creates a file inside the `migration` folder.

## debugging

With the following command, we wan watch the SQL code that will be run to the database.

`python3 manage.py sqlmigrate blog 0001`

This saves us a lot of time, we only use the model class and Django writes the SQL itself.

## running the migration

Migrations allow us to update our database without messing with the data.
Let's run the migration command

`python3 manage.py migrate`

We could also write python code by accessing the shell.

`python3 manage.py shell`

From the shell we can easily access the database.
// NOTE: FIND REFERENCE AND DOCUMENTATION

We can also write python commands directly from our `view.py` file

```py
from .models import Post

def home(request):
  context = {
    'posts': Post.objects.all()
  }
  return render(request, 'blog/home.html', context)
```
