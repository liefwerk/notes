# Login and Logout System

From our urls.py of the main project, we import the auth_views.
We also add the new urls for the login and logout.
Thi includes the path to the templates we'll use to generate the HTML.

```py
from django.contrib.auth import views as auth_views

urlpatterns = [
    path('login/', auth_views.LoginView.as_view(template_name='users/login.html'), name='login'),
    path('logout/', auth_views.LogoutView.as_view(template_name='users/logout.html'), name='logout'),
]
```

Here's a snippet of code from our login.html templates

```django
{% extends 'blog/base.html' %} {% load crispy_forms_tags %} {% block content %}
<div class="content-section">
    <form method="POST">
        {% csrf_token %}
        <fieldset class="form-group">
            <legend class="border-bottom mb-4">Log In</legend>
            {{ form|crispy }}
        </fieldset>
        <div class="form-group">
            <button class="btn btn-outline-info" type="submit">Login In</button>
        </div>
    </form>
    <div class="border-top pt-3">
        <small class="text-muted">
            Need an account ? <a class="ml-2" href="{% url 'register' %}">Sign Up Now</a>
          </small>
    </div>
</div>
{% endblock content %}
```

We can redirect our users to the main page of our blog by editing the settings.py page
We'll add this snippet of code:

`LOGIN_REDIRECT_URL = 'blog-home'`
