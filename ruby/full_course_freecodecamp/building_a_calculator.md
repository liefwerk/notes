# building_a_calculator

Let's build a very basic calculator. We get the two numbers from the user and we print out the sum.

When you enter information into an input, Ruby will identify it as a string.
To add two numbers, we convert the strings into numbers (with the method `.to_i`)

```ruby
puts "Enter the first number"
num1 = gets.chomp()
puts "Enter the second number"
num2 = gets.chomp()
puts (num1.to_i + num2.to_i)
```

The issue with this solution it that it converts the strings into integers.
That won't take the decimals into consideration. `.to_f` is the right solution.

```ruby
puts "Enter the first number"
num1 = gets.chomp()
puts "Enter the second number"
num2 = gets.chomp()
puts (num1.to_f + num2.to_f)
```

We could also add the method after the variable `gets` method.

```ruby
num1 = gets.chomp().to_f
```
