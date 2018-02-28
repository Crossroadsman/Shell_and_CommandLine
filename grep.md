grep
====

regular expression parser

Examples
--------


### All lines that include 'the' in a file ###
(note that things like 'whether' will be returned as matches (but 'Then' will not). Use '\Wthe\W' to exclude those sorts of hits)
```
grep -n "the" myfile.txt
```

Notes:
1. `-n` will prepend line numbers
2. " and ' are equivalent for surrounding the string

Other useful flags:
- `-i` - case insensitive
- `-v` - invert results (show all non-matching lines instead of matching lines)

## All lines containing at least one word of at least 6 characters ###
```
grep -E "\w{6,}" myfile.txt
```

Regex Variants
--------------

grep can be called with several different flags to specify the kind of regular expressions that will be matched:

- `-E` : **'extended'**
- `-G` : **'basic'** (this is the default)
- `-P` : **'perl'** (experimental)

Per the Man page, in GNU grep there is no difference in functionality between basic and extended. However, in practice, there are some 
differences in syntax.

For example, the following command:

```
grep -E "\w{6,}" myfile.txt
```

will return any lines containing any sequences of at least 6 word characters. In contrast:

```
grep -G "\w{6,}" myfile.txt
```

will return any lines containing the literal characters `w{6,}`.
