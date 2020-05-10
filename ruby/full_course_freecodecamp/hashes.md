# hashes

A hash is a type of data structure wehre we store different peices of information.
Very similar to an array. The difference is that we can store a key value pair.

A key value pair is a value that we store with a key (name).

Hashes are also called dictionnaries. Eeach words has a definition, the word is the key and the definition is the value.

Let's build a hash that stores US Codes.

To create an hash, we give it a name

```
states = {
    "Pennsylvania" => "PA",
    "New York" => "NY",
    "Oregon" => "OR"
}
```

Each value can only have one key.

Then we can print it out:

```
puts states["Oregon"]
```

and that will print

```
OR
```

Alternatively, we could format the keys this way

```
states = {
    :Pennsylvania => "PA",
    :New York => "NY",
    :Oregon => "OR"
}
```