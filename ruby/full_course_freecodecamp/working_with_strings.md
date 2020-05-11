# working_with_strings

There a a few methods that we can call to modify, give more info about the string.

To print out a string:

```ruby
puts "my string is going to be printed"
```

To print a quotation mark

```ruby
puts "Here\'s a quotation mark!"
```

To print out a new line

```ruby
puts "this is going to \na new line"
```

and that prints

```ruby
this is going to
a new line
```

Using a variable

```ruby
phrase = "my phrase is in a variable !"
puts phrase
```

## Methods

**`upcase()` to change the text's format**

```ruby
phrase = "my phrase is in a variable !"
puts phrase.upcase()
```

**`strip()` to delete things from the string**

```ruby
phrase = "     my phrase as a lot of space !     "
puts phrase.strip()
```

**`include()` asks if there the phrase includes the values that we pass inside it**

```ruby
phrase = "where is waldo?"
puts phrase.include? "waldo"
```

that prints out

```ruby
true
```
