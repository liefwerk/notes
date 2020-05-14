# Running the server

Running the server with Django is very easy, from the command line we write

`python3 manage.py runserver`

That opens the website in a browser at `http://localhost:8001/`

We can also access `http://localhost:8001/admin`

This page is setup on the `urls.py` file.

Here's a example

``` python
from django.conf.urls import url
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', admin.site.urls),
]
```
