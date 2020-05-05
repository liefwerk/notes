# math_and_numbers

To use a number in Ruby is super easy

```
puts 3
puts 4.983
puts -947
```

Basic math also works

```
puts 5+4
puts 3/4
puts 2**3
```

that last one is a way to put the number to the raised power like 2^3.

```
puts 10 % 3
```

that will spit our the remainder

```
1
```

If we want to print a number paired with a string, we have to convert that number into a string.

```
num = 12
puts ("my favorite number is " + num.to_s)
```

## The Math class

Methods to help us do more operations

```
num = 12
puts math.sqrt(36)
```

There are two types of numbers, integers and floating numbers.
Once you add a floating point, you'll get a floating point printed. Otherwise it will stay an integer.