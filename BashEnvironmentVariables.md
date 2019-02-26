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

### Definitions ###

- "interactive": Not a shell script
- "login": Involve passing credentials to initiate the session (e.g., `ssh` or `su - <username`)

Thus:
- a typical local terminal session (e.g., launching Terminal.app in macOS) is *interactive* *non-login*;
- a remote `ssh` session is *interactive* *login*;
- a shell script (including login/startup script?) is *non-interactive* *non-login*;
- ??? is *non-interactive* *login*

Startup Script Sequence
-----------------------
1. `/etc/profile` (applies to all users);
2. `/etc/profile.d/*` (alphabetically, applies to all users);
3. `~/.profile`

Note, Bash, for interactive login (or non-interactive with the `--login` option) sessions loads in this order (see 
`man bash`):

1. `/etc/profile` (if it exists);
2. The first, and only first, file found when searching in the following order:
  a. `~/.bash_profile`;
  b. `~/.bash_login`; then
  c. `~/.profile`

and for interactive non-login sessions (again from `man bash`) loads in this order:

1. `/etc/bash.bashrc`; then
2. `~/.bashrc`

Note that there is also `/etc/environment` for setting global environment variables. This is *read* but not *sourced*
(i.e., variable definitions are set but commands are not executed).

Purposes
--------
(see <https://superuser.com/a/183956>)

### `~/.profile` ###
Traditionally, this was the place to define per-user environment variables for shells.

### `~/.bash_profile` ###
The Bash-specific equivalent to `~/.profile`. By default this is an all-or-nothing substitute for `.profile`. If Bash
finds this file it will load this instead of `~/.profile`.

### `~/.bashrc` ###
For non-login-related items. Note, on some systems (Debian and most derivatives), `~/.profile` sources `~/.bashrc` so these
items will be inherited by login shells as well. On such systems this is the default place to put things. Things like
command aliases and functions.

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

We can see environment variables using `printenv` and (environment variables + shell 
variables + shell functions) using `set` or `declare`.

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

`set -x` prints commands and their arguments as they are executed. Turning
this option on is a good first step for debugging a script, as it shows how
the Bash has interpreted and expanded its input.

Using declare without any args shows all variables and functions

```console
$ declare
Apple_PubSub_Socket_Render=/private/tmp/com.apple.launchd.vdWh6uG7Q6/Render
BASH=/usr/local/bin/bash
BASHOPTS=checkwinsize:cmdhist:complete_fullquote:expand_aliases:extquote:force_fignore:globasciiranges:hostcomplete:interactive_comments:login_shell:progcomp:promptvars:sourcepath
BASH_ALIASES=()
BASH_ARGC=([0]="0")
BASH_ARGV=()
BASH_CMDS=()
BASH_LINENO=()
BASH_REMATCH=([0]="x")
BASH_SOURCE=()
...
```

Using `-p` prints the values of all variables in the current environment, 
along with some short option flags that describe their properties.

```console
$ declare -p
declare -x Apple_PubSub_Socket_Render="/private/tmp/com.apple.launchd.vdWh6uG7Q6/Render"
declare -- BASH="/usr/local/bin/bash"
declare -r BASHOPTS="checkwinsize:cmdhist:complete_fullquote:expand_aliases:extquote:force_fignore:globasciiranges:hostcomplete:interactive_comments:login_shell:progcomp:promptvars:sourcepath"
declare -i BASHPID
declare -A BASH_ALIASES=()
declare -a BASH_ARGC=([0]="0")
declare -a BASH_ARGV=()
declare -- BASH_ARGV0
declare -A BASH_CMDS=()
declare -- BASH_COMMAND
...
```

Using `-f` prints the values of all functions in the current environment:

```console
$ declare -f
__nvm () 
{ 
    declare previous_word;
    previous_word="${COMP_WORDS[COMP_CWORD - 1]}";
    case "${previous_word}" in 
        use | run | exec | ls | list | uninstall)
            __nvm_installed_nodes
        ;;
        alias | unalias)
            __nvm_alias
...
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
