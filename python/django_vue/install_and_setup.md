# Install and setup

## Django setup
### Setting up the environment for Chongo

First we create an environment with Python in our chosen directory: `virtualenv env_3_8_5`

We then activate the environment, this will prepend the environment to our command line so if we use `pip install` it will only install it for our environment: `source env_3_8_5/bin/activate`

### Installing Django

We then install Django and few dependencies:

- `django-rest-framework` will help us create the api
- `django-cors-headers` helps with the security of the api
- `djoser` helps managing the creation and login of users with tokens
- `pillow` helps with resizing images
- `stripe` handles the payments

```
pip install django
pip install django-rest-framework
pip install django-cors-headers
pip install djoser
pip install pillow
pip install stripe
```

We now create a new project.

```
django-admin startproject djackets_django
cd djackets_django
```

### Settings of our project

Before we start we have to go to `settings.py` and add these few lines to the `INSTALLED_APPS` list.

```python
'rest_framework',
'rest_framework.authtoken',
'corsheaders',
'djoser',
```

We also add this list below:

```python
CORS_ALLOWED_ORIGINS = [
    "http://localhost:8080",
]
```

And finally in the `MIDDLEWARE` list we add one line. It should be just after the `SessionMiddleware` and before the `CommonMiddleware`.

```python
'corsheaders.middleware.CorsMiddleware',
```

Then we head up to `url.py`, add `inlude` to our imports and add two new paths to handle the users.

```python
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    # our new paths below
    path('api/v1/', include('djoser.urls')),
    path('api/v1/', include('djoser.urls.authtoken')),
]
```

### Initialising the database

The first step is to create the migrations files with `python3 manage.py makemigrations`.

Now create a new database already filled with tables by typing `python3 manage.py migrate`.

To test everything we'll create a superuser and login to our admin page. It will prompt you with a few questions regarding the username, email and password you want to use.

To create a superuser just run this command: `python3 manage.py createsuperuser`

Lastly, we have to run the server to login. http://localhost:8000/admin

## Vue setup

Go back one level up the tree and run `vue create djackets_vue`.

This prompts us a few choices. First, we'll choose `Babel`, `Router`, `Vuex` and `CSS pre-processors`. Then we go with Vue 3. We'll also use the history mode for the router. We prefer using dart/sass ass a pre-processor. Finally, we will store all this in dedicated config files.

When our installation is finished, we can then go to the created directory `cd djackets_vue`.

###  Adding a few dependencies

We then install Django and few dependencies:

- `axios` will help us talk with the backend
- `bulma` is a CSS library similar to Bootstrap

```
yarn add axios
yarn add bulma
```

### Testing our front-end

To test the front end we just have to run the following command: `npm run serve`.

## Including FontAwesome

We'll include this library inside our vue project in `public/index.html`. Add the next line below our `<title></title>` tag.

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css">
```

