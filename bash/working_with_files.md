# Working with files

## mkdir - Making a directory

`mkdir` will create one of several directories.

```bash
mkdir Junk
cd Junk
```

## touch - Creating and updating files

If you use the touch command with an existing file, it will update the date.
If you touch a file that doesn't exist, it will create it.

```bash
touch file1 file2 file3
ls
```

## cp - Copy files

`cp` copies a file.
We could create a backup really easily.

```bash
cp ~/.bashrc bashrc.bak
```

## mv - Move a file

`mv` is used to move and rename a file

```bash
mv bashrc.bak bashrc
```

We could also move the content of the file

```bash
mv bashrc file1
```

The file bashrc doesn't exist anymore and it's content is in file1.

## rm - Remove files and directories

There aren't any undo button when you use it.
Be careful!

```bash
rm file2
```

To give it more power, we can use a wildcard.
`*` will remove everything.

```bash
rm *
```

`file*` will remove any file that starts with `file`.

```bash
rm file*
```

### rm -r - Remote directories

This put `rm` in a recursive mode.
That is very powerful and can remove everything.

```bash
rm -r dir1
```

`rmdir` only removes directories, so it only works when there aren't any files inside it.
Very useful to remove all empty directories in one shot.

```bash
rmdir dir2
```
