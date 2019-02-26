Test (/`[`/`[[`)
================

The `test` command is used to evaluate conditional expressions.
The full syntax is available with `help test`.

Example:
```console
$ test -e /etc/passwd && echo 'Password file exists!'
Password file exists!
```

`[` is an equivalent command (that takes `]` as a terminating argument):

```console
$ [ -e /etc/passwd ] && echo 'Password file exists!'
Password file exists!
```

Both `test` and `[` are builtins (with equivalent external programs):

```console
$ type -a test
test is a shell builtin
test is /bin/test
$ type -a [
[ is a shell builtin
[ is /bin/[
```

The more sophisticated `[[` works similarly but is a keyword rather than a
builtin or executable:

```console
$ type -a [[
[[ is a shell keyword
```

`[[` is like a `[` but with more functionality. Generally, `[` commands work
the same in `[[` but `[[` offers additional arguments that are unavailable to
`[`.

Example:
```shell
#!/usr/bin/env bash

if [[ -e customers ]] ; then
    printf 'Customers file already exists, renaming...\n'
    mv customers customers-old
fi
mv customers-new customers
```
