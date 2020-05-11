# inheritance

What if we have a class and we want to make another one with slighlty different attributes or outputs ?

```ruby
class Chef
  def make_chicken
    puts "The chef makes chicken"
  end
  def make_salad
    puts "The chef makes salad"
  end
  def make_spacial_dish
    puts "The chef makes bbq ribs"
  end
end

class ItalianChef

end
```

We have a Chef and Italian Chef. The Italian Chef can do the same things as our first Chef.
In order to pass the methods we do this `< Inheritance`

```ruby
class ItalianChef < Chef

end
```

We can also override an inherited method and add a new one

```ruby
class ItalianChef < Chef
    def make_special_dish
       puts "The chef makes pizza"
    end
    def make_pasta
        puts "The chef makes pasta"
    end
end
```
