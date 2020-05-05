# building_mad_libs_game

A Mad Lib Game is a type of game that would switch the words inside a sentence.
We can easily build that with a few lines of code.

```
puts "Roses are {color}"
puts "{plural_noun} are blue"
puts "I love {celebrity}"
```

First let's get the input from the user

```
puts "Enter a color"
color = gets.chomp()
puts "Enter a plural noun"
plural_noun = gets.chomp()
puts "Enter a celebrity name"
celebrity = gets.chomp()
```

Now we have all three inputs. We then add the variables.

```
puts "Enter a color"
color = gets.chomp()
puts "Enter a plural noun"
plural_noun = gets.chomp()
puts "Enter a celebrity name"
celebrity = gets.chomp()

puts ("Roses are " + color)
puts (plural_noun + " are blue")
puts ("I love " + celebrity)
```