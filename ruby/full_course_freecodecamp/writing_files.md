# writing_files

Let's write information to files.
We'll use another file mode to do that.

```
File.open("employee.txt", "r") do |file|

end
```

[Here's a reference from github](https://stackoverflow.com/questions/7085595/file-opening-mode-in-ruby/7085623#7085623)

```
File.open("index.html", "w") do |file|
    file.write("<h1>Hello</h1>")
end
```

We have to be careful when we modify a file, each time the program is launched, it will modify it.