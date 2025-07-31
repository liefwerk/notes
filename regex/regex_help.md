# Help with RegEx

RegEx is hard. At least I'm having issue with it.

Here's some tips (that will improve with time) to help myself - and maybe other.

## Match before and after a single character

This expression matches any character before and after the word password, if it is in between double quotes.

```regex
/".*password.*"/gi
```

### Same but without space between the word

```regex
/"password"/gi
```

## Match any line with characters present in a list

In this example we want to match lines that have [INF] or [WRN].

The (?:...) creates a non-capturing group. Since we're not using the captured group content (just checking if the pattern matches), this avoids the overhead of capturing and storing the matched text.

```regex
/^\[(?:INF|WRN)\]/g
```

## Split from a list of characters

The list of characters are either <*>, <*...>, <~...>, <=...>, <-...> or even a combination of all such as <-=-*-~->

```regex
<[*~=\-]*>
```