# arrays

Let's use arrays in Ruby.
One way to keep track of data is using variables, but what if we want to store more ?

Here come the arrays! Let's create one.

```
friends = Array["John", "Ryu", "Yoshi"]
```

To access one element, we use the index of the array

```
friends = Array["John", "Ryu", "Yoshi"]
puts friends[0]
```

To create an array without specifying data inside, we do this

```
friends = Array.new
friends[0] = "Ryu"
```