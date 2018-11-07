Bash and Environment Variables
==============================

Where Bash Looks for Permanent Environment Variables
----------------------------------------------------

 Shell Type |      Interactive      |    Non-Interactive
------------|-----------------------|---------------------
Login       | <ol><li>`/etc/profile`</li><li>`~/.bash_profile`</li><li>`~/.bash_login`</li><li>`~/.profile`</li></ol>     | <ol><li>`/etc/profile`</li><li>`~/.bash_profile`</li><li>`~/.bash_login`</li><li>`~/.profile`</li></ol>
Non-Login   | <ol><li>`/etc/bash.bashrc`</li><li>`~/.bashrc`</li></ol> | `$BASH_ENV`


**Note: Although .bashrc is not necessarily executed on login, it is common for .profile or .bash_profile to include a line prompting
.bashrc to be loaded. Accordingly, an environment variable can be set in .bashrc and .bash_profile can execute .bashrc so the variable
only needs to be set in one place.**

Formatting Environment Variables
--------------------------------

### `VAR` vs `$VAR` vs `${VAR}` ###

`VAR` is the name of the variable, `$VAR` and `${VAR}` are ways of expanding that variable. In most situations, the use of these are
equivalent, but there are situations where the latter leads to a different result. Consider the [following][link01] example:

Suppose `VAR` contains the string 'FOO' and we wanted to combine it with 'BAR'. Trying to do the following:
```
$VARBAR
```
wouldn't work, since it would try to expand the variable `VARBAR`. Similarly:
```
$VAR BAR
```
wouldn't work, since it would place a space character between 'FOO' and 'BAR'. Thus we do:
```
${VAR}BAR
```
which produces 'FOOBAR'.

Kinds of Variables
------------------

- `shell`: limited to the current shell session (not passed to children)
- `environment`: passed to children

We can see environment variables using `printenv` and (environment variables + shell variables + shell functions) using `set`.

Example usage of `printenv`:
```console
$ printenv
LANG=en_us.UTF-8
EDITOR=vim
HOME=/home/user
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin...etc
...
```

Reading a single environment variable:
```console
$ printenv EDITOR
vim
```

### Comparison of shell and environment variables ###

```console
$ TEST_VAR = 'Hello world!'  # This creates a shell variable
$ printenv | grep -E "TEST"  # doesn't appear in printenv
$ set | grep -E "TEST"       # does appear in set
TEST_VAR='Hello World!'
```

```console
$ echo $TEST_VAR
Hello world!
$ bash
$ echo $TEST_VAR  # doesn't appear because wasn't passed to child shell
```

```console
$ exit             # return to parent shell
exit
$ export TEST_VAR  # promote TEST_VAR to environment variable
$ bash
$ echo $TEST_VAR   # does appear because environment variable was passed to child
Hello world!
```

We can demote an environment variable down to a shell variable:
```console
$ export -n TEST_VAR
```

Or unset it completely (applies to either environment or shell variables):
```console
$ unset TEST_VAR
```


Note we can also inline a variable and it will only exist for the associated command:
```console
$ STAGING_URL=staging.example.com:8000 python3 manage.py test functional_tests
```
This will run the command `python3 manage.py test functional_tests` and only this command will see the variable `STAGING_URL`



[link01]: https://stackoverflow.com/questions/1416024/bash-path-and-path
