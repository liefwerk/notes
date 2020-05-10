# if_statements

If statements work as follow:

```
ismale = true

if ismale
    puts "Your are male!"
end
```

`else` statements can handle other scenarios

```
ismale = true

if ismale
    puts "Your are male!"
else
    puts "You are not male."
end
```

we could also work with two contitions with the word `and`

```
ismale = true
istall = true

if ismale and istall
    puts "Your are male!"
end
```

the word `or` will choose between two conditions
the word `elseif` will check another condition
the word `!` means not, in context `!ismale` means not male

## Using comparisons

We can compoare different values inside the if statement.

Let's create a methods called max. It will take numbers and return the largest one.

```
def max(num1, num2, num3)
    
end
```