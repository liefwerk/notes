# Serializer and views for the products

The Serializer is where we get the information from the database and turn in into JSON so we can use it in the front end. To create it we go to our django app and create a file called `serializer.py`.

```python
from rest_framework import serializers
from .models import Category, Product

# We create a new Serializer class
class ProductSerializer(serializers.ModelSerializer):
    # We also create a Meta class
    class Meta:
        # to link it to the Product class
        model = Product
        # We add the fields we want to serialize
        fields = (
            "id",
            "name",
            "get_absolute_url",
            "description",
            "price",
            "get_image",
            "get_thumbnail"
        )
```

Then we go to `views.py` so we can tell django what we want to put in our model.

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .models import Product
from .serializer import ProductSerializer

class LatestProductsList(APIView):
    def get(self, request, format=None):
        products = Product.objects.all()[0:4]
        serializer = ProductSerializer(products, many=True)
        return Response(serializer.data)
```

Next step is to create a separate `urls.py` file to keep everything tidy.

```python
from django.urls import path, include
from product import views

urlpatterns = [
  [[create_django_app_and_models]] create_django_app_and_models.md  path('latest-products/', views.LatestProductsList.as_view()),
]
```

Then we add this new pattern to the main `urls.py`.

```python
urlpatterns = [
    ...
    path('api/v1/', include('product.urls')),
] + ...
```

If we visit the following url `http://localhost:8000/api/v1/latest-products/` we can view that we actually don't have any product in our database. To create some product we can head to the file named `admin.py` in the app folder. We'll import the Models and register them in the admin side.

```python
from .models import Category, Product

admin.site.register(Category)
admin.site.register(Product)
```

We can launch the admin part with `http://localhost:8000/admin` and create categories and products.