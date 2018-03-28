Misc Facts and Notes About Bash
===============================

[Shell Syntax / Operation][link01]
----------------------------------

1. Read input from
   - file;
   - string supplied as an argument to the `-c` invocation option; or
   - from user's terminal input;
2. Break the input into tokens (*words* and *operators*); perform *alias expansion*
3. Parse the tokens into commands
4. Perform *shell expansions*
5. Perform redirections (and remove redirection operators and operands from the argument list)
6. Execute the command
7. (Optionally) wait for the command to complete and collect its exit status






[link01]: https://www.gnu.org/software/bash/manual/bash.html#Shell-Operation
