`pushd`, `popd`, `dirs`
=======================

`pushd`
-------

### `pushd <dirname>` ###

Pushes `<dirname>` onto the top of the `{dirs}` (the current 
directory history?) stack and changes to that directory.

Example:

```console
~ $ cd old
old $ pushd ~/new
~/new ~/old
new $
```

Note that manually `cd`ing to a directory will pop the stack and push the 
directory `cd`'d to.

Example (continues from previous example):

```console
new $ cd
~ $
~ $ pushd other
~/other ~ ~/old
other $
```
Note that `~/new` is no longer on the stack. The `cd` to home put the home
directory on the top of the stack. Then pushing `~/other` put that to the top
of the stack.

We can have duplicates on the stack.

Example (continues from previous example):

```console
other $ cd
~ $ pushd foo
~/foo ~ ~ ~/old
foo $
```

Observe that the home directory was added to the stack, even though it was
already top of the stack.

### `pushd +<n>` ###

Brings the directory at index `<n>` to the top of the stack and moves to that
directory. Rotates the stack.

Example:

```console
baz $ dirs -v
0 ~/baz
1 ~/bar
2 ~/foo
3 ~
baz $ pushd +2
~/foo ~ ~/baz ~/bar
```


`popd`
------

Pops the `{dirs}` stack and moves to the directory that was next in the stack.

Example:

```console
~ $ pushd foo
~/foo ~ ~ ~/old
foo $ popd
~
```

### `popd +<n>` ###

Remove the dir at index `<n>` (doesn't change current directory).

Example:

```console
baz $ dirs -v
0 ~/baz
1 ~/bar
2 ~/foo
3 ~
baz $ popd +2
~/baz ~/bar ~
```


dirs
----

Show the directory stack.

Use the `-v` option to print the contents vertically with index numbers; use
the `-c` option to clear the stack.
