# Create, Update and Delete Posts

## Showing individual posts

Within our blog app, we'll open up `view.py`
We'll create a class based views.

```py
from django.views.generic import ListView

class PostListView(ListView):
    model = Post
    template_name = 'blog/home.html'  # <app>/<model>_<viewtype>.html
    context_object_name = 'posts'
    # this orders the posts by date
    ordering = ['-date_posted']
```

Then inside our urls.py file

```py
from .views import PostListView

# there we store our urls
urlpatterns = [
  # our class based view takes a methods called as_view()
    path('', PostListView.as_view(), name='blog-home')
]
```

Now we'll create a Detail View to view each single posts

```py
from django.views.generic import ListView, DetailView

class PostDetailView(DetailView):
    model = Post
```

We can now add the path to the new post detail view

```py
from .views import PostListView, PostDetailView

path('post/<int:pk>/', PostDetailView.as_view(), name='post-detail'),
```

We then create the html template at `templates/blog/post_details.html`

```django
{% extends "blog/base.html" %}
{% block content %}
    <article class="media content-section">
        <img class="rounded-circle article-img" src="{{ object.author.profile.image.url }}">
        <div class="media-body">
            <div class="article-metadata">
                <a class="mr-2" href="#">{{ object.author }}</a>
                <small class="text-muted">{{ object.date_posted|date:"F d, Y" }}</small>
            </div>
            <h2 class="article-title">{{ object.title }}</h2>
            <p class="article-content">{{ object.content }}</p>
        </div>
    </article>
{% endblock content %}
```

And we update the link in the home.html page to include the individual posts

`href="{% url 'post-detail' post.id %}"`

## Creating a new post

In the views.py, we keep adding the generic view to then modify some parts of it.
We'll also add a mixin to require a logged in user.

```py
from django.contrib.auth.mixins import LoginRequiredMixin, UserPassesTestMixin
from django.views.generic import (
    ListView,
    DetailView,
    CreateView,
    UpdateView,
    DeleteView
)
```

Then, we add the view in ours blog `urls.py`

```py
from .views import (
    PostListView,
    PostDetailView,
    PostCreateView,
    PostUpdateView,
    PostDeleteView
)
```

And we add the path

```py
urlpatterns = [
    path('post/new/', PostCreateView.as_view(), name='post-create'),
]
```

That also means that we'll create a new template, it's name will be the one expected by django: `post_form.html`

Here's the code for the template

```django
{% extends 'blog/base.html' %}
{% load crispy_forms_tags %}
{% block content %}
<div class="content-section">
    <form method="POST">
        {% csrf_token %}
        <fieldset class="form-group">
            <legend class="border-bottom mb-4">Blog Post</legend>
            {{ form|crispy }}
        </fieldset>
        <div class="form-group">
            <button class="btn btn-outline-info" type="submit">Post</button>
        </div>
    </form>
</div>
{% endblock content %}
```

## Updating a new post

If we want to update a post, the process is very similar.
In `view.py` we import the basic view and we modify it.

Notice that we'll also add a `form_valid()` funtion.
That is because we want to point the current user as the updater.
We also have a `test_func` method, it will check if the current user
is the original post's author.

```py
class PostUpdateView(LoginRequiredMixin, UserPassesTestMixin, UpdateView):
    model = Post
    fields = ['title', 'content']

    def form_valid(self, form):
        form.instance.author = self.request.user
        return super().form_valid(form)

    def test_func(self):
        post = self.get_object()
        if self.request.user == post.author:
            return True
        return False
```

In urls.py we also add the new view in the imports and add the new path
This time, our path takes the pk (id) of a single post.

```py
path('post/<int:pk>/update/', PostUpdateView.as_view(), name='post-update'),
```

### Adding the button

To access the new `post-update` view we'll add a link to the template of a detail view of each post

```django
{% if object.author == user %}
    <div>
        # the pk of each individual post will be added through that {% url 'post-update' object.id %}
        <a href="{% url 'post-update' object.id %}" class="btn btn-secondary btn-sm my-1">Update</a>
        <a href="{% url 'post-delete' object.id %}" class="btn btn-danger btn-sm my-1">Delete</a>
    </div>
{% endif %}
```

## Deleting a Post

Also very similar to updating a post, but we won't have the `form_valid()` method this time.

```py
class PostDeleteView(LoginRequiredMixin, UserPassesTestMixin, DeleteView):
    model = Post
    success_url = '/'

    def test_func(self):
        post = self.get_object()
        if self.request.user == post.author:
            return True
        return False
```

In urls.py we also add the new view in the imports and add the new path
This time, our path takes the pk (id) of a single post.

```py
path('post/<int:pk>/delete/', PostDeleteView.as_view(), name='post-delete'),
```
