# User Registration

We'll first create a new app named users to hanlde all that logic separatly.

`python3 manage.py startapp users`

From the `views.py` of the new user app, we'll import a form and render it inside our template

```py
from django.shortcuts import render
from django.contrib.auth.forms import UserCreationForm

def register(request):
  form = UserCreationForm()
  return render(request, 'users/register.html', {'form': form})
```

## Adding the form

We can 'supercharge' the form, making its UI closer to a bootstrap styling.
First, in `settings.py` we'll add this line of code to the installed apps

`'crispy_forms',`

We can now add the form inside the template `register.html`

```django
{% extends 'blog/base.html' %} {% load crispy_forms_tags %} {% block content %}
<form method="POST">
    {% csrf_token %}
    <fieldset class="form-group">
        <legend class="border-bottom mb-4">Join Today</legend>
        {{ form|crispy }}
    </fieldset>
    <div class="form-group">
        <button class="btn btn-outline-info" type="submit">Sign Up</button>
    </div>
</form>
```

## Form logic

We'll also add the logic of the form to our `users/views.py`

```py
from django.shortcuts import render, redirect
from django.contrib import messages
from .forms import UserRegisterForm

def register(request):
  if request.method == 'POST':
    form = UserRegisterForm(request.POST)
    if form.is_valid():
      form.save()
      # username = form.cleaned_data.get('username')
      messages.success(request, f'Your account has been created! You are now able to log in.')
      return redirect('login')
  else:
    form = UserRegisterForm()
  return render(request, 'users/register.html', {'form': form})
```
