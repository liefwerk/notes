# Templates

We use template to avoid retyping the same html code over and over.

## Create a template

To create a template we simply create a folder in our app called `templates` then another with the same name as the app

In our example:

```text
django_project
  blog // our app
    migrations
    templates
      blog // our templates go here
  django_project // our main project
```

## Link the template

In order for django to search for template and models, we add it to the `settings.py` file

```python
INSTALLED_APPS = [
    'blog.apps.BlogConfig',
    ...
```

Then in `views.py` we tell django to look at our template file for Home

```python
# here we load the render method
from django.shortcuts import render

def home(request):
  # we render our home.html template
  return render(request, 'blog/home.html')
```

## Add data to our template

To add data, we have to pass it to the page's `render()` method in `views.py`.

```python
# dictionnary with dummy posts
posts = [
  {
    'author': 'John Snow',
    'title': 'Blog Post 1',
    'content': 'First post content',
    'date_posted:': 'August 27, 2081'
  },
  {
    'author': 'Jane Doe',
    'title': 'Blog Post 2',
    'content': 'Second post content',
    'date_posted:': 'August 28, 2081'
  },
]

def home(request):
  # dictionnary with differents keys
  context = {
    # unique key
    'posts': posts
  }
  # then we pass the context dictionnary inside the render method
  return render(request, 'blog/home.html', context)
```

Then we go to our template home.html file and loop over these posts.

```htmldjango
{% for post in posts %}
  <h1>{{ post.title }}</h1>
  <p>By {{ post.author }} on {{ post.date_posted }}</p>
  <p>{{ post.content }}</p>
{% endfor %}
```

## Template inheritance

When we have repeated code throughout our application, it's good practice to find write it only once and reuse it later.
We can create a structure with a base.html template and write a block in which we'll be able to overwrite with the other template.

We create base.html and paste this inside

```htmldjango
{% block content %}
{% endblock %}
```

Then we go in the other template in which we'll write the other part of the HTML

```htmldjango
{% extends 'blog/base.html' %}
{% block content %}
  # there we place our html
{% endblock content %}
```
