# Pagination

Pagination is useful when we don't want to show all the posts when the page is loaded.

## Adding more posts

First, let's add more posts.
We'll have a posts.json file which we'll update to our database.
And we'll do that with the python shell.

```python shell
import json
from blog.models import Post
with open('posts.json') as f:
  posts_json = json.load(f)

for post in posts_json:
  post = Post(title=post['title'], content=post['content'], author_id=post['user_id'])
  post.save()

exit()
```

## Adding the pagination

In the `view.py` file of our blog, we'll add an attribute to the `PostListView`

```py
class PostListView(ListView):
    model = Post
    template_name = 'blog/home.html'  # <app>/<model>_<viewtype>.html
    context_object_name = 'posts'
    ordering = ['-date_posted']
    # new attribute
    paginate_by = 5
```

Now, in our home.html template we'll add some if logic to show the appropriate buttons

```django
{% if is_paginated %}
  {% if page_obj.has_previous %}
    <a class="btn btn-outline-info mb-4" href="?page=1">First</a>
    <a class="btn btn-outline-info mb-4" href="?page={{ page_obj.previous_page_number }}">Previous</a>
  {% endif %}
  {% for num in page_obj.paginator.page_range %}
    {% if page_obj.number == num %}
      <a class="btn btn-info mb-4" href="?page={{ num }}">{{ num }}</a>
    {% elif num > page_obj.number|add:'-3' and num < page_obj.number|add:'3' %}
      <a class="btn btn-outline-info mb-4" href="?page={{ num }}">{{ num }}</a>
    {% endif %}
  {% endfor %}
  {% if page_obj.has_next %}
    <a class="btn btn-outline-info mb-4" href="{{ page_obj.next_page_number }}">Next</a>
    <a class="btn btn-outline-info mb-4" href="?page={{ page_obj.paginator.num_pages }}">Last</a>
  {% endif %}
{% endif %}
```

## Creation of a User Post View

We want to create a view for each athor in which we'll see their posts.

Let's add the logic for the view in `view.py`

```py
from django.shortcuts import get_object_or_404
from django.contrib.auth.models import User

class UserPostListView(ListView):
    model = Post
    template_name = 'blog/user_posts.html'
    context_object_name = 'posts'
    paginate_by = 5

    def get_queryset(self):
        user = get_object_or_404(User, username=self.kwargs.get('username'))
        return Post.objects.filter(author=user).order_by('-date_posted')
```

Then we add the url to our `urls.py` file

```py
from .views import (
  ...
  UserPostListView
)

# there we store our urls
urlpatterns = [
    ...
    # our new path
    path('user/<str:username>', UserPostListView.as_view(), name='user-posts'),
    ...
]
```

Now, in our templates we'll add the right link to the user `<a></a>` tag
This is the case for each template that has the name of the author:

- home.html
- post_detail.html
- user_posts.html

```django
<a class="mr-2" href="{% url 'user-posts' post.author.username %}">{{ post.author }}</a>
```
