Misc Facts and Notes About [Bash][title01]
==========================================

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

[Escaping and Quoting][link02]
------------------------------

- `\` (non-quoted backslash): the Bash escape character. It preserves the literal value of the next character that follows (except 
                              *newline*: a `\`*newline* pair represents line continuation)
- `'` (single quotes): Enclosing characters in single quotes preserves the literal value of each character. Note that a single quote 
                       character can never be represented in the string within the single quotes (even if escaped)
- `"` (double quotes): Enclosing characters in double quotes preserves the literal value of most characters. Special characters:
    - `$`
    - \`
    - `\`<sup>[1](#footnote01)</sup>
    - `!`<sup>[2](#footnote02)</sup>
    - `*`
    - `@`

[Lists of Commands][link03]
---------------------------

- `command1 && command2` AND list: *command2* is executed iff *command1* returns an exit status 0
- `command1 || command2` OR<sup>[3](#footnote03)</sup> list: *command2* is executed iff *command1* returns an exit status not 0

See also [this](https://askubuntu.com/a/817969) Ask Ubuntu answer which provides more interesting commentary on chaining commands.



Footnotes
----------
<a name="footnote01">1</a>: Only retains special meaning if followed by `$`, 'backtick', `"`, `\`, or *newline*  
<a name="footnote02">2</a>: Only when history expansion is enabled and shell is not in Posix mode
<a name="footnote03">3</a>: It is called 'OR' but is really XOR

[title01]: https://www.gnu.org/software/bash/manual/bash.html#SEC_Contents
[link01]: https://www.gnu.org/software/bash/manual/bash.html#Shell-Operation
[link02]: https://www.gnu.org/software/bash/manual/bash.html#Quoting
[link03]: https://www.gnu.org/software/bash/manual/bash.html#Lists
