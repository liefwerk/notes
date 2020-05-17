# User Profile and Picture

## Creating the User model

How can we add more functionnality to our Users ?
First, let's create a new User model in our `users/models.py` file

Since we'll expand the existing model, we'll import it

`from django.contrib.auth.models import User`

```py
class Profile(models.Model):
  user = models.OneToOneField(User, on_delete=models.CASCADE)
  # CASCADE means when the user is deleted, the profile will be deleted
  # but when the profile is deleted, our user won't.
  image = models.ImageField(default='default.jpg', upload_to='profile_pics')

  def __str__(self):
    return f'{self.user.username} Profile'
```

To use the method ImageField we need `Pillow`, se let's install it with pip3

`pip3 install Pillow`

### Importing the model to the database

Then we'll confirm the model by migrating it to the database

`python3 manage.py makemigrations`

then

`python3 manage.py migrate`

### Registering the model

We also have to register the model in our `users/admin.py` file

```py
from .models import Profile

admin.site.register(Profile)
```

### Adding a new path

Let's add some more settings in the settings.py file.
This will allow us to use the path `/media` to store images for the profiles.

```py
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media'
```

## Profile

### Creating the profile view

Then we create `profile.html` to have a template for our profile page

```django
{% extends 'blog/base.html' %} {% load crispy_forms_tags %} {% block content %}
<div class="content-section">
    <div class="media">
        <img class="rounded-circle account-img" src="{{ user.profile.image.url }}">
        <div class="media-body">
            <h2 class="account-heading">{{ user.username }}</h2>
            <p class="text-secondary">{{ user.email }}</p>
        </div>
    </div>
    <!-- FORM HERE -->
</div>

{% endblock content %}
```

### Serving the Profil view

Now, in our user view we'll add that new logic

```py
# we'll use a decotator to make that page only visible to loggedin users
from django.contrib.auth.decorators import login_required

@login_required
def profile(request):
  return render(request, 'users/profile.html')
  ```

### Adding the urlpattern for the images

In urls.py we'll add the urlpattern

```py
from django.conf import settings
from django.conf.urls.static import static

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

## Creating a Signal

Let's create a new file called `signals.py` at the root of our `users` folder

```py
from django.db.models.signals import post_save
from django.contrib.auth.models import User
from django.dispatch import receiver
from .models import Profile

# we want a user pfoile created for the creation of each user
@receiver(post_save, sender=User)
def create_profile(send, instance, created, **kwargs):
  if created:
    Profile.objects.create(user=instance)

@receiver(post_save, sender=User)
def save_profile(send, instance, **kwargs):
  instance.profile.save()
```

Then in apps.py of our users app, we add it to the config

```py
class UsersConfig(AppConfig):
    name = 'users'

    def ready(self):
        import users.signals
```
