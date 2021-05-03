# better_calculator

```ruby
puts "Enter first number: "
num1 = gets.chomp().to_f
puts "Enter the operator"
op = gets.chomp()
puts "Enter second number: "
num2 = gets.chomp().to_f

if op == "+"
  puts (num1 + num2)
elsif op == "-"
  puts (num1 - num2)
elsif op == "*"
  puts (num1 * num2)
elsif op == "/"
  puts (num1 / num2)
else
  puts "Fuck, an error!"
end
```

Let' s not forget to use `==` and put `end` at the end of the function
