# return_statement

Why don't we write a cube function to demostrate how the return statement works.

```
def cube(num)

return num * num * num    

end

puts cube(2)
```

that prints

```
8
```

We can also return several values inside the same method

```
def cube(num)

return num * num * num, 40

end

puts cube(4)
```

that prints

```
2  
40
```

we can also individually access the return statements

```
puts cube(4)[1]
```

that prints

```
40
```