# getting_user_input

To get info from the user, we have to the terminal.
This is the code that we'll prompt to the terminal to get that user data.

```ruby
puts "Enter your name: "
name = gets
puts ("Hello " + name)
```

Then the terminal prompts `Enter Your Name:`

Everytime we press the key `Enter` that registers it as an input and Ruby will put a new line.
In order to prevent this default action we use the method `.chomp()`

```ruby
puts "Enter your name: "
name = gets.chomp()
puts ("Hello " + name + ", you are noice!")
```
