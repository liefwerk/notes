# Working with text files

Using linux means working a lot with text files.

## cat - List everything

```bash
cat file1
```

Anything that cat comes up with goes to this file.
You'll type anything you want then hit `ctrl+D` to escape.

```bash
cat >> file2
cat file2
```

cat also prints the content of multiple files at the same time.

## more, less - Other way to look inside a file

`more` is very old, you'll page through the text in the terminal.
`Q` is also for leaving.

```bash
more file1
```

`less` is more than more. We can use arrow keys, scan back up, search for text.
`Q` is also for leaving.

```bash
less file1
```

## nano - Very powerful little text editor

`Ctrl+O` to write out the file.
`Ctrl+X` to exit.

```bash
nano file2
```

## Direction

### cat >> - Appending to an existing file

With `cat > file2` we create a new file called `file2`.
With `cat >> file2` we append to `file2`.

### | - Piping

Taking the output of a file and putting it in another.

```bash
history | less
```

Let's say we want to see everything of this directory, list it and put it in a file.
We'll list the root directory and put it inside a file.

```bash
ls -la / > lsout.txt
```
