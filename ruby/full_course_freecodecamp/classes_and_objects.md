# classes_and_objects

Ruby allows us to use a wide range of types of data.
We can easily represent and use them, but not all real world  objects can be reprensented with just a boolean, string or number.

Here come the objects and classes.

Ruby allows us to create our own data type.
We can create a class (custom data type) this way:

```ruby
class Book
    attr_accessor :title, :author, :pages
end
```

We can now create a book object to represent an individual book.

```ruby
book1 = Book.new()
book1.title = "Harry Potter"
book1.author = "JK Rowling"
book1.pages = 403
```

It allows us to interact with the object

```ruby
puts books.title
puts books.pages
```

that prints

```ruby
Harry Potter
403
```
