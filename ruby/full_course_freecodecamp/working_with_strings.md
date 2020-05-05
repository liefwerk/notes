# working_with_strings

There a a few methods that we can call to modify, give more info about the string.

To print out a string:

```
puts "my string is going to be printed"
```

To print a quotation mark

```
puts "Here\'s a quotation mark!"
```

To print out a new line

```
puts "this is going to \na new line"
```

and that prints

```
this is going to 
a new line
```

Using a variable

```
phrase = "my phrase is in a variable !"
puts phrase
```

## Methods

**`upcase()` to change the text's format**

```
phrase = "my phrase is in a variable !"
puts phrase.upcase()
```

**`strip()` to delete things from the string**

```
phrase = "     my phrase as a lot of space !     "
puts phrase.strip()
```

**`include()` asks if there the phrase includes the values that we pass inside it**

```
phrase = "where is waldo?"
puts phrase.include? "waldo"
```

that prints out

```
true
```