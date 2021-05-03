# modules

In module we can store different classes and methods

```ruby
module Tools

    def sayhi(name)
        puts "Hello #{name}"
    end
    def sayby(name)
        puts "Bye #{name}"
    end
end

include Tools

Tools.sayhi("Mike")
```

If we want to export that module from another file, we first need to require the file

```ruby
require_relative "module.rb"
include Tools

Tools.sayby("Nat")
```
