# Application and Routing

Within our website we could have different apps.

A single project can contain multiple apps.
We could take a single app and add it to multiple parts of the main website.

## Creation of an app

Let's create our blog app with the command line

`python3 manage.py startapp blog`

## Setting up the Routing

Let's naviguate to that new directory and go to view.python
We import django.http

`from django.http import HttpReponse`

We then setup a function to handle the visit of a user at the main page of our blog.
Let's go to views.py and add this bit of code:

```python
def home(request):
  return HttpResponse('<h1>Blog Home</h1>')
```

We then create a `urls.py` file and populate it with this snippet of code to start.

```python
from django.shortcuts import render
from django.http import HttpResponse

def home(request):
  return HttpResponse('<h1>Blog Home</h1>')
```

Now if we go to `http://localhost:8001/blog/` we'll get that `<h1>Blog Home</h1>`.

To add a new page, that's quite easy, from our `views.py` we add a new function

```python
def about(request):
  return HttpResponse('<h1>Blog About</h1>')
```

and we add that to the `urls.py` file

```python
def about(request):
  return HttpResponse('<h1>Blog About</h1>')

```

Now, what if we want our /blog be our root / ?
We just set it up on urls.py

```python
urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url('', include('blog.urls'))
]
```
