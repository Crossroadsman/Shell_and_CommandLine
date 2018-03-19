sed
===

Applies a regular expression to a text file (or a stream).

Syntax
------

Basic syntax is in the form:

```
sed <transformation> <target>
```

**Notes**:
- `<transformation>` is the regex to apply
- `<target>` is the combination of stream/file in/out

Examples:

1:

```
sed 's/hello/world/' input.txt > output.txt
```

Reads the contents of `input.txt` and replaces instances of 'hello' with 'world' then writes the revised text to `output.txt`.


