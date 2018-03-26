awk
===

awk is a special purpose programming language for processing text files

versions
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
