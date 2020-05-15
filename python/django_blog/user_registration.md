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

We can now add the form inside the template `register.html`

```django
<form method="POST">
    {% csrf_token %}
    <fieldset class="form-group">
        <legend class="border-bottom mb-4">Join Today</legend>
        {{ form.as_p }}
    </fieldset>
    <div class="form-group">
        <button class="btn btn-outline-info" type="submit">Sign Up</button>
    </div>
</form>
```

## Supercharging the form

I'll add this tomorrow.
