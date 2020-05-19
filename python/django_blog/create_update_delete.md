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

I'll add this later
