# reading_files

We can easily read files inside our program.

First, we load the file using the `File.open()` method

```ruby
File.open("employee.txt", "r") do |file|

end
```

`"r"` means we only want to read it, there are other modes with which we can interact with the file
`do |file|` means that we store it inside a variable called `file`

Then we can apply all string methods available in Ruby.
