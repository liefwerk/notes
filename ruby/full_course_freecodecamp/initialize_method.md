# initialize_method

An initialize method is a method that will be called everytime we initialize an object.
The class is a blueprint and when we create an object we give it some default information.

```ruby
class Book
    attr_accessor :title, :author, :pages
    def initialize(title, author, pages)
    @title = title
    @author = author
    @pages = pages
       puts "Creating Book"
    end
end
```

Everytime we create an object from this class, the initialize method will be called.

```ruby
book1 = Book.new("Harry Potter", "JK Rowling", 403)
```
