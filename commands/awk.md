awk
===

[awk][link01] is the name of a special purpose programming language for processing text files. It is also the name of the program that 
you use to create instructions in this language.

Versions
--------
Historically, awk is divided into 'old' awk and 'new' awk.

Additionally, new awk is often used to describe either Unix awk (the true awk) or the almost completely compatible gnu version of awk: gawk.

You can check if you are running new or old awk by trying the following test program:

```awk
awk 1 /dev/null
```

New awk will silently run the program, while old awk will produce an error message along the lines of:

```awk
error-> awk: syntax error near line 1
error-> awk: bailing out near line 1
```

Language Syntax
---------------

An awk program consists of a series of *rules*, each *rule* specifies a *pattern* to search for, and an action to perform on finding that
pattern (enclosed in braces), as in the following:

```awk
pattern { action }
pattern { action }
...
```

Running an awk Program
----------------------
There are two main ways of running an awk program, either in-line, such as the following:
```
awk 'program' input-file1 input-file2 ...
```

Or by putting the awk program in a file and then running that:
```
awk -f program-file input-file1 input-file2 ...
```

Note that running awk without specifying any input files will cause awk to be applied to standard in.




[link01]: https://www.gnu.org/software/gawk/manual/gawk.html#Foreword3
