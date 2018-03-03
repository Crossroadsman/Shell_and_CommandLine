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


[link01]: https://stackoverflow.com/questions/1416024/bash-path-and-path
