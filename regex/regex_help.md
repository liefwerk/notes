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
/<[*~=\-]*>/g
```

## Matching then grouping

Something to understand is the difference between a match and a group.

Let's say you have the following line: `[WRN] User James123 has exceeded storage space.`.
With this line you want to EXTRACT the string that is after the word User. It needs to account for one or multiple spaces.
In this example, the string we want to extract is `James123`.

```regex
/User\s+(\w+)/g
```

Here we want to start matching User with one of multiple spaces with `User` and `\s+`.
Then, we start making a capturing group with `()`, and that capturing group needs to only be a full string (which can also be seen as a full word).
In that case, we need to add `\w+` inside the brackets.

The final form is `User\s+(\w+)`, the capturing group gives us the full username from the line.