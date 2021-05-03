# while_loops

```ruby
index = 1
while index <=  5
    puts index
    index += 1
end
```

## building a guessing game

We let the user keep guessing the word until they find it.

```ruby
secret_word = "coronavirus"
guess = ""

while guess != secret_word
  puts "guess my word"
  guess = gets.chomp()
end

puts "Well done !"
```

But what if we put a guess limit ?

```ruby
# guessing game

secret_word = "coronavirus"
guess = ""
guess_count = 0
guess_limit = 3
out_of_guesses = false

while guess != secret_word and !out_of_guesses
  if guess_count < guess_limit
    puts "guess my word:"
    guess = gets.chomp()
    guess_count += 1
  else
    out_of_guesses = true
    return puts "Fat chance, you are out of guesses!"
  end
end

puts "Well done !"
```
