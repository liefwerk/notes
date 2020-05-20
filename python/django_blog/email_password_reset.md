# Email and Password Reset

## Password Reset View

Within our file `urls.py` of the `django_project` folder we'll create a few path using
already made views.

```py
urlpatterns = [
    ...
    path('password-reset/',
      auth_views.PasswordResetView.as_view(
          template_name='users/password_reset.html'
      ),
      name='password_reset'),
    ...

]
```

Then we create a new template called `password_reset.html`

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
            <button class="btn btn-outline-info" type="submit">Request Password Reset</button>
        </div>
    </form>
</div>
{% endblock content %}
```

## Password Reset Done View

Then we create a path to redirect the user to tell him that it's password was successfuly changed.
In urls.py we add this code for the `password_reset_done` view

```py
urlpatterns = [
    ...
    path('password-reset/done/',
      auth_views.PasswordResetDoneView.as_view(
          template_name='users/password_reset_done.html'
      ),
      name='password_reset_done'),
    ...

]
```

Then we create it's template

```django
{% extends 'blog/base.html' %} {% block content %}
  <div class="alert alert-info">
    An email has been sent with instructions to reset your password.
  </div>
{% endblock content %}
```

## Password Reset Confirm View

Now we need to create a route for `password_reset_confirm`

```py
urlpatterns = [
    ...
    path('password-reset-confirm/<uidb64>/<token>/',
      auth_views.PasswordResetConfirmView.as_view(
          template_name='users/password_reset_confirm.html'
      ),
      name='password_reset_confirm'),
    ...

]
```

Let's create the template for this view, it'll use a form.

```py
{% extends 'blog/base.html' %} {% load crispy_forms_tags %} {% block content %}
<div class="content-section">
    <form method="POST">
        {% csrf_token %}
        <fieldset class="form-group">
            <legend class="border-bottom mb-4">Reset Password</legend>
            {{ form|crispy }}
        </fieldset>
        <div class="form-group">
            <button class="btn btn-outline-info" type="submit">Reset Password Now</button>
        </div>
    </form>
</div>
{% endblock content %}
```

## Password Reset Complete View

Now we need to create a route for `password_reset_complete`

```py
urlpatterns = [
    ...
    path('password-reset-confirm/<uidb64>/<token>/',
      auth_views.PasswordResetConfirmView.as_view(
          template_name='users/password_reset_confirm.html'
      ),
      name='password_reset_confirm'),
    ...

]
```

Let's create the template for this view, it'll be very similar to the `password_reset_done` view

```py
{% extends 'blog/base.html' %} {% block content %}
  <div class="alert alert-info">
    Your password has been set.
  </div>
  <a href="{% url 'login' %}">Sign In Here</a>
{% endblock content %}
```

Finally, we can add a link to the `reset_password` view in our `login.html` template

```django
<small class="text-muted ml-2">
    <a href="{% url 'password_reset' %}">Forgot Password ?</a>
</small>
```
