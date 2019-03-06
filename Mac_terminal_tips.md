Mac Terminal Tips
=================

Tips that work with Apple's built-in Terminal app (may not work with iTerm).

Paste escaped text into terminal
--------------------------------

CTRL-V will paste regular text. Modify this with CMD to paste escaped text
Similarly, dragging text into Terminal will paste regular, CMD-dragging will paste escaped.

(source: @jnadeau and @ChrisPage Twitter)


Highlight the result of the most recent operation
-------------------------------------------------
Do the command (e.g., pwd, ls, etc)

then CMD-shift-A

(source: @brentsimmons Twitter)


Place the cursor with the mouse
-------------------------------

Option-click

(Source: @eholtam Twitter)

Open
----
Use `open` to work like a double-click in the Finder.

For example to load an app bundle:
```console
$ open /Applications/Safari.app/
```

To load a file in whatever app is registered:
```console
$ open file_image.jpg
```

You can use `-a <application>` to specify a particular app or
`-e` to force the file to be opened in TextEdit. `-t` forces the file
to be opened in whichever text editor is registered with LauncServices.

pbcopy / pbpaste
----------------

Copy to the clipboard / paste from the clipboard.

Examples:
```console
$ ls ~ | pbcopy
```

Will pipe the output of `ls` on the user's home directory into the
clipboard.

```console
$ pbcopy < some_file.txt
```

Read the contents of `some_file.txt` into the clipboard.

```console
$ pbpaste >> some_list.txt
```

Append the contents of the clipboard to the file `some_list.txt`.
