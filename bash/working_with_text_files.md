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
