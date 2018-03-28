tar
===

Compatibility
-------------

`tar` on macOS is BSDTar which is subtly different to Gnu tar on Linux.

gnutar is no longer distributed as standard with macOS but can be obtained through homebrew. Similarly, bsdtar is available using most 
package managers on Linux.


Usage
-----

### Creating an archive ###

#### On macOS: ####

To create a gzip-compressed file:
```
tar -zcvf <archive_name.tar.gz> <folder_to_archive>
```
or to create a bzip-compressed file:
```
tar -jcvf <archive_name.tar.bz2> <folder_to_archive>
```

where:
- `-z` : compress using gzip
- `-j` : compress using bzip2
- `-c` : create archive
- `-v` : verbose
- `-f` : filename (followed by the archive filename)

#### On Linux: ####

To create a gzip-compressed file:
```
tar -cavf <archive_name.tar.gz> <folder_to_archive>
```
or to create a bzip-compressed file:
```
tar -cavf <archive_name.tar.bz2> <folder_to_archive>
```

where:
- `-a` : auto-detect compression by reference to specified archive name extension
- `-c` : create archive
- `-v` : verbose
- `-f` : filename (followed by the archive filename)

### Extract an archive ###

```
tar -xvf <archive_file>
```

Both Mac and Linux should be able to detect the compression type.


### A Note About Compression ###

Typically bzip2 creates slightly smaller files than gzip (though not always, and occasionally can create larger files than gzip) but
is significantly slower.


### A Note About File Locations ###

Sometimes the archive must be untarred and installed from a particular location (e.g., the user's home directory, or `/`, or `/usr/src`, 
etc). If this is the case, there is likely to be an error during the untar process and more clues can usually be found in the package's
documentation (e.g., `README` or `Install` files).

