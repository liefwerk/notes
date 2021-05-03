# methods

To define a methods we do it like this

```ruby
def task_name

end
```

Here's an example

```ruby
def sayhi
    puts "Hi Mark!"
end
```

To execute the code inside wa have to call it.

```ruby
sayhi
```

## Variables inside the method

We can pass variables inside the method

```ruby
def sayhi(name)
puts ("Hi " + name)
end

sayhi("Mark")
```

## Default variables

```ruby
def sayhi(name="no name", age=-1)
puts ("Hi " + name + ", your age is " + age.to_s)
end

sayhi("Mark")
```
