Tee
===

tee takes an input and sends the output to a specified file and stdout

Traditionally the purpose of this command has been to send output to both a file and stdout at the same time.

The most common modern use is to take a program output that has regular user privileges and to write it to a file that requires sudo access.

Example
-------

Consider the following example<sup>[1](#footnote01)</sup> where we are executing a program with sudo privileges and want to write the output 
of that to a file that also requires sudo privileges:

```
sudo ls -la /root/ > /root/output.txt
```

The intent of the above command is obvious, with root access get a listing of the files in `/root/` and write that list to a file in root's
home directory.

However, this won't work because although `ls` was run with sudo privileges, the redirect doesn't have sudo privileges, and so the regular
user is unable to write the file to root's home directory.

We can use `tee` to get around this by piping the output of ls into tee (calling tee with sudo) and then a superuser tee is able to write 
the file:

```
sudo ls -la /root/ | sudo tee /root/output.txt > /dev/null
```

**Notes**:
1. `/root/output.txt` is the file we are outputting to
2. `> /dev/null` redirects the output from the stdout (which in this case means screen) to null (so we are explicit about not displaying
   the output)








<a name="footnote01">1</a>: Based on the example from Stack Overflow: <https://stackoverflow.com/questions/82256/how-do-i-use-sudo-to-redirect-output-to-a-location-i-dont-have-permission-to-wr>
