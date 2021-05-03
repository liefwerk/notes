# Show individual orders for users

Let's learn how to show individual orders. let's first create a new serializer. Go to `serializer.py` and add the following classes.

```python
class MyOrderItemSerializer(serializers.ModelSerializer):
    # using the product ad the object
    product = ProductSerializer()

    class Meta:
        model = OrderItem
        fields = (
            "price",
            "product",
            "quantity",
        )

class MyOrderSerializer(serializers.ModelSerializer):
    # this is quite similar to the order serializer, without the create function
    items = MyOrderItemSerializer(many=True)

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
            # adding paid amount as a variable
            "paid_amount"
        )
```

Now to create a view set for the my orders page.

```python
from .serializers import OrderSerializer, MyOrderSerializer

...
class OrdersList(APIView):
    # getting authentication
    authentication_classes = [authentication.TokenAuthentication]
    permission_classes = [permissions.IsAuthenticated]

    def get(self, request, format=None):
        # user is the requested user (which is authenticated)
        orders = Order.objects.filter(user=request.user)
        # using the my order serializer
        serializer = MyOrderSerializer(orders, many=True)
        return Response(serializer.data)
```

Next, import it to the `urls.py` file in the same folder.

```python
urlpatterns = [
    ...
    path('orders/', views.OrdersList.as_view()),  
]
```

## Handling the front-end

Go to `MyAccount.vue` and add the following code below the log out button.

```javascript
<hr>
<div class="column is-12">
    <h2 class="subtitle">My orders</h2>

    <OrderSummary
        v-for="order in orders"
        v-bind:key="order.id"
        v-bind:order="order" />
</div>
```