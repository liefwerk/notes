# for_loops

Very useful to loop inside a collection.

```ruby
friends = ["Thomas", "Amaury", "Yann", "Maxence", "Antoine", "Alexandre"]

for friend in friends
    puts friend
end
```

It also is possible to loop through it with `.each`

```ruby
friends.each do |friend|
    puts friend
end
```

If we want to choose the number of times we want to loop

```ruby
for index in 0..5
    puts index
end
```

that prints

```ruby
0
1
2
3
4
5
```

Alternatively, we could write

```ruby
6.times do |index|
    puts index
end
```

that prints **the same output**
