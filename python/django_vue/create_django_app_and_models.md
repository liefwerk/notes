# Creating the Django App and the models

## Creating a new app and a new class

In order to create our Django App named product we write in the terminal: `python3 manage.py startapp product`. This will create a new `product` folder in the `djackets_django` folder.

We'll first visit and modify the  `models.py` file. In this file we are going to create our first class called `Category`.

```python
# our new class
class Category(models.Model):
    
  # it contains two variables
  # name is the name of the category
  name = models.CharField(max_length=255)
  # slug zill be used in the url
  slug = models.SlugField()

  # we'll apply some ordering with the meta subclass
  class Meta:
    ordering = ('name',)
    
  def __str__(self):
    return self.name

  # This function return the url of the category
  def get_absolute_url(self):
    return f'/{self.slug}/'
```

Then we need to tell django that this app exists. Let's head to `settings.py` and add the following to the `INSTALLEd_APPS` list. `'product'`.

## Making the migration

Just like we did the first time we created the database, we'll first write the following command `python3 manage.py makemigrations`. It returns that Django needs to create a new model named `Category`.

We can then write `python3 manage.py migrate` to update the database with our model.

## Creating the Products Model

The next model is a bit more complicated because it involves a few other librairies for the images.

Here's the code we can append to the `models.py` file:

```python
# our new product class
class Product(models.Model):
  # these are the fields we'll use and their parameters
  category = models.ForeignKey(Category, related_name='products', on_delete=models.CASCADE)
  name = models.CharField(max_length=255)
  slug = models.SlugField()
  description = models.TextField(blank=True, null=True)
  price = models.DecimalField(max_digits=6, decimal_places=2)
  image = models.ImageField(upload_to='uploads/', blank=True, null=True)
  thumbnail = models.ImageField(upload_to='uploads/', blank=True, null=True)
  date_added = models.DateTimeField(auto_now_add=True)

  # we'll also reuse the next three functions for this class
  class Meta:
    ordering = ('-date_added',)

  def __str__(self):
    return self.name

  def get_absolute_url(self):
    return f'/{self.category.slug}/{self.slug}/'

  # this is a new function that returns the url of the product's image 
  def get_image(self):
    if self.image:
      return 'http://localhost:8000' + self.image.url
    return ''

  # this returns the thumbnail of the product's image
  # it also builds it using the make_thumnail function below
  def get_thumbnail(self):
    if self.thumbnail:
      return 'http://localhost:8000' + self.thumbnail.url
    else:
      if self.image:
        self.thumbnail = self.make_thumbnail(self.image)
        self.save()

        return 'http://localhost:8000' + self.thumbnail.url
      else:
        return ''
  
  # this function makes a thumbnail out of an image we pass through it
  def make_thumbnail(self, image, size=(300, 200)):
    img = Image.open(image)
    img.convert('RGB')
    img.thumbnail(size)

    thumb_io = BytesIO()
    img.save(thumb_io, 'JPEG', quality=85)

    thumbnail = File(thumb_io, name=image.name)

    return thumbnail
```

## Adding the media folders to Django

To add a new folder we go to `settings.py` and add the new lines below the `Static files` section:

```python
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media/'
```

We finish this step by going to `urls.py` and adding `settings` and `static`:

```python
from django.conf import settings
from django.conf.urls.static import static
...

urlpatterns = [
   ...
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```