# exception_handling

How can we handle the errors ?

```ruby
# error 1
num = 10 / 0

```

We can catch an error so that the program won't crash.

```ruby
begin
    # inside any code that might throw an error
rescue
    # this will be executed if that goes wrong
end
```

We can also name the error if we have a few different lines that could catch different errors.

```ruby
begin
    # inside any code that might throw an error
rescue TypeError => e
    # this will be executed if that goes wrong
    puts e
end
```
