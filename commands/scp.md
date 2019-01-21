scp (secure copy)
=================


Syntax (BSD version, as available on MacOS and Ubuntu 18.10<sup>[1](#footnote01)</sup>)
-----------------------------------------------------------
```console
$ scp [-346BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file] [-l limit]
      [-o ssh_option] [-P port] [-S program] source ... target
```
Where most common options/parameters:
- `-r`: recursively copy directories. Symlinks will be followed if traversed in
  the tree;
- `source` and `target` can each be specified as:
  - local pathname (using absolute or relative pathnames)  
    e.g., `/home/my_user/file.ext` or `../other_dir/other_file.ext`;
  - remote host with optional path in the form `[user@]host:[path]`
    e.g., `my_host.com:` or `192.168.1.14:` or `user2@my_host.com:/home/user2`;
  - URI in the form `scp://[user@]host[:port][/path]  
    e.g., `scp://user2@my_host.com:8000/home/user2` or 
    `scp://u3@host2.com/home/u3`.  
  Note that in the host/path example, the `:` is used as a separator between
  host and path, while in the URI example, the `:` is used as an (optional) 
  port specifier.

Other options/parameters:
- `-3`: copies between two remote hosts are routed through the local host;
- `-4`: force use of IPv4 addresses only;
- `-6`: force use of IPv6 addresses only;
- `-B`: Batch mode (prevents asking for passwords/passphrases);
- `-C`: Enable compression (option is passed to ssh);
- `-c cipher`: Use the specified cipher (option passed directly to ssh);
- `-F ssh_config`: Specifies an alternative per-user configuration file for 
  ssh (option passed directly to ssh);
- `-i identity_file`: Specifies an identity (private key) for using public
  key authentication (option passed directly to ssh);
- `-l limit`: Limit bandwidth (specified in Kbit/s);
- `-o ssh_option`: Used to pass other options to ssh (in the format used in
  ssh_config);
- `-P port`: Specify remote host port;
- `-p`: Preserve modification metadata from original files;
- `-q`: Quiet mode (suppress progress meter and warning/diagnostic messages);
- `-S program`: name of alternative connection encryption program. Must be
  compatible with ssh options;
- `-v`: verbose mode (for both scp and ssh)


Examples
--------

### Transfer a local file to remote host ###

- Background Data
  ```console
  ~$ pwd
  /home/user1
  ~$ ls -la
  drwxr-xr-x 11 user1 user1  4096 Jan 21 11:56 .
  drwxr-xr-x  3 root  root   4096 Dec 11 12:54 ..
  -rw-r--r--  1 user1 user1  4009 Dec 11 16:40 .bashrc
  drwxr-xr-x  2 user1 user1  4096 Jan 21 11:56 my_files
  ```

- Actual Transfer
  ```console
  ~$ scp -r my_files user2@my_host.com:/path/to/files
  ```

### Transfer a remote file to the host ###
```console
$ scp -r user2@my_host.com:/home/user2/other_files .
```


See Also
--------
[BSD scp Man Page](https://www.freebsd.org/cgi/man.cgi?query=scp&sektion=1)
[Linux – How to Securely Copy Files Using SCP examples](https://haydenjames.io/linux-securely-copy-files-using-scp/)


**Questions and Todos**
-----------------------
- If no remote path is supplied, where (if anywhere) do the files end up?
- Presumably could use `&` to do in background, is this true?
- Need to verify example remote to local.


Footnotes
---------
1. <a name="footnote01"> </a>Version as per `lsb_release -a`
