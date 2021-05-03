# Handling Stripe

The first step is to create an account at [stripe.com](https://stripe.com).

## Storing the API credentials

Go to `settings.py` in the `Django` main folder and add the following code.

```python
STRIPE_SECRET_KEY = 'SECRET_KEY'
```

## Creating the Order class

Then to track of the orders, let's create a new folder with startapp: `python3 manage.py startapp order`. Add it on the INSTALLED_APPS in the `settings.py` file.

```python
INSTALLED_APPS = [
    ...
    'product',
    'order'
]
```

In the freshly created `/order` folder, go to models.py and add the following code.

```python
# we import the User model
from django.contrib.auth.models import User
from django.db import models

# we import the Product model
from product.models import Product

class Order(models.Model):
  # we add the User as a ForeignKey and name it orders
  user = models.ForeignKey(User, related_name='orders', on_delete=models.CASCADE)
  # Here are the fields we'll use
  first_name = models.CharField(max_length=100)
  last_name = models.CharField(max_length=100)
  email = models.CharField(max_length=100)
  address = models.CharField(max_length=100)
  zipcode = models.CharField(max_length=100)
  place = models.CharField(max_length=100)
  phone = models.CharField(max_length=100)
  # useful to get the current time and date
  created_at = models.DateTimeField(auto_now_add=True)
  # what has been paid
  paid_amount = models.DecimalField(max_digits=8, decimal_places=2, blank=True, null=True)
  # the stripe token in case we need it later
  stripe_token = models.CharField(max_length=100)

class Meta:
    # this orders the orders with the date, so it's easier to see it in the backend
    ordering = ['-created_at',]

  def __str__(self):
    # this return the first name of the user who created the order when we call the Order
    return self.first_name

# getting each item as a separate entity as well
class OrderItem(models.Model):
  # referencing to the order
  order = models.ForeignKey(Order, related_name='items', on_delete=models.CASCADE)
  # referencing to the product to know which product it is on the item
  product = models.ForeignKey(Product, related_name='items', on_delete=models.CASCADE)
  # to easily get the price without going through the product
  price = models.DecimalField(max_digits=8, decimal_places=2)
  # quantity defaults to 1
  quantity = models.IntegerField(default=1)

  def __str__(self):
    return '%s' % self.id
```

Now let's apply this changes to the database with: `python3 manage.py makemigrations` and `python3 manage.py migrate`.

## Adding the Django views

Go to `order/views.py`.

```python
import stripe

# for accessing the api secret from settings.py
from django.conf import settings
# need the USERS
from django.contrib.auth.models import User
# for errors
from django.http import Http404
from django.shortcuts import render

# import a few funtions from the framework
from rest_framework import status, authentication, permissions
from rest_framework.decorators import api_view, authentication_classes, permission_classes
from rest_framework.views import APIView
from rest_framework.response import Response

# importing the models
from .models import Order, OrderItem
# importing the serializers for the order models
from .serializers import OrderSerializer, MyOrderSerializer

# this view only handles POST Requests
@api_view(['POST'])
# authentication because we want to require authentication from the user
@authentication_classes([authentication.TokenAuthentication])
@permission_classes([permissions.IsAuthenticated])
# checkout function, pass the request
def checkout(request):
    # we get the data from the request and pass it thorugh the serializer
    serializer = OrderSerializer(data=request.data)

    # if it is valid
    if serializer.is_valid():
        # we pass the key to stripe
        stripe.api_key = settings.STRIPE_SECRET_KEY
        # we set the paid amount to the total price*quantity of each product
        # we do this for every item validated through the serializer
        paid_amount = sum(item.get('quantity') * item.get('product').price for item in serializer.validated_data['items'])

        # we'll accept or show an error if the error is succesfful or not
        try:
            # cratting a charge for stripe
            charge = stripe.Charge.create(
                # we multiply by 100 because stripe wants it in cents and not in dollars
                amount=int(paid_amount * 100),
                currency='USD',
                description='Charge from Djackets',
                # stripe token we get from the token
                source=serializer.validated_data['stripe_token']
            )
            # when we go through this, it means that everything works
            serializer.save(user=request.user, paid_amount=paid_amount)
            # return the response to tel the frontend that it works
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        # if something is wrong
        except Exception:
            # return an error to show in the front end
            return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
    # else we show another error
    return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```

## Adding the handling of stripe to the urls

Go to `order/urls.py` to register the new view.

```python
from django.urls import path
from order import views

urlpatterns = [
    path('checkout/', views.checkout) 
]
```

## Creating the serializer for the order

Create a file named `serializer.py` in the `order/` folder.

```python
from rest_framework import serializers
# we want to models of the order
from .models import Order, OrderItem
# also need the secralizers used for creating the products
from product.serializers import ProductSerializer

# the serializer for the order item
class MyOrderItemSerializer(serializers.ModelSerializer):    
    product = ProductSerializer()

    class Meta:
        model = OrderItem
        # the fields we need
        fields = (
            "price",
            "product",
            "quantity",
        )

# the serializer for the order
class MyOrderSerializer(serializers.ModelSerializer):
    # to get the items we use the previous serializer
    items = MyOrderItemSerializer(many=True)

    class Meta:
        model = Order
        # the fields we need
        fields = (
            "id",
            "first_name",
            "last_name",
            "email",
            "address",
            "zipcode",
            "place",
            "phone",
            "stripe_token",
            "items",
            "paid_amount"
        )

class OrderItemSerializer(serializers.ModelSerializer):    
    class Meta:
        model = OrderItem
        fields = (
            "price",
            "product",
            "quantity",
        )

class OrderSerializer(serializers.ModelSerializer):
    items = OrderItemSerializer(many=True)

    class Meta:
        model = Order
        fields = (
            "id",
            "first_name",
            "last_name",
            "email",
            "address",
            "zipcode",
            "place",
            "phone",
            "stripe_token",
            "items",
        )
    
    # function used for creating an order
    # passing itself and the validated data through it
    def create(self, validated_data):
        # we remove the items from the validated_data
        items_data = validated_data.pop('items')
        # we create a new order based on the validated data we get from the form
        order = Order.objects.create(**validated_data)

        # we loop through all of the items
        for item_data in items_data:
            # we create a new order item
            # set the order (a foreign key) to that item data
            # the product is already included (**item_data)
            OrderItem.objects.create(order=order, **item_data)
            
        return order
```

## Getting the token in the front-end

In `Checkout.vue`, add the following function to the methods. This function called `stripeTokenHandler` is being called through another function named `submitForm` once the okten has been created on the back-end.

```javascript
async stripeTokenHandler(token){
    const items = [];

    for (let i = 0; i < this.cart.items.length; i++) {
        const item = this.cart.items[i]
        const obj = {
          product: item.product.id,
          quantity: item.quantity,
          price: item.product.price * item.quantity
        }
        items.push(obj)
    }

    const data = {
        'first_name': this.first_name,
        'last_name': this.last_name,
        'email': this.email,
        'address': this.address,
        'zipcode': this.zipcode,
        'place': this.place,
        'phone': this.phone,
        'items': items,
        'stripe_token': token.id
    }

    await axios
        .post('/api/v1/checkout/', data)
        .then(response => {
            // clearing the cart
            this.$store.commit('clearCart')
            // redirecting to the success page
            this.$router.push('/cart/success')
        })
        .catch(error => {
            this.errors.push('Something went wrong. Please try again')
            console.log(error)
        })
        this.$store.commit('setIsLoading', false)

}
```

Do not forget to add the order urls to the main `urls.py`.

```python
urlpatterns = [
    ...
    path('api/v1/', include('order.urls')),
]
```

### Importing Stripe in the front end

Inside the `mounted` hook.

```javascript
import {loadStripe} from '@stripe/stripe-js';
...
// if we have products in the cart
if (this.cartTotalLength > 0) {
    // new instance of stripe
    this.stripe = await loadStripe('pk_test_51H1HiuKBJV2qfWbD2gQe6aqanfw6Eyul5PO2KeOuSRlUMuaV4TxEtaQyzr9DbLITSZweL7XjK3p74swcGYrE2qEX00Hz7GmhMI')
    // new instance of elements
    const elements = this.stripe.elements();
    //
    this.card = elements.create('card', { hidePostalCode: true })
    this.card.mount('#card-element')
}
```

Importing stripe is quite easy, just follow the instruction from [the stripe documentation](https://stripe.com/docs/libraries).

Let's also add the `clearCart` function in the store.

```javascript
clearCart(state) {
    state.cart = { items: [] }
    localStorage.setItem('cart', JSON.stringify(state.cart))
},
```

### Registering the orders in the Django administration

Load the `admin.py` in the `order/` folder.

```python
from django.contrib import admin
from .models import Order, OrderItem

admin.site.register(Order)
```