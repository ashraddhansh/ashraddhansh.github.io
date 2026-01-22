+++
title = "File Types in Unix Based OSs"
date = 2019-11-27
+++

This is my first blog post.
There are 7 types of files in a UNIX like environment:
1. Regular File
2. Directories
3. Character device files
4. Block device files
5. Local domain sockets
6. Named pipes(FIFOs)
7. Symbolic links
# Determining File Types using `ls` 
You can determine the file type of an existing file with `ls -ld` 
- The flag `-l` displays detailed information about the file or directory like permission, number of links, owner, group, size etc.
- Flag `-d` prevents ls from listing the content of directories, instead it shows the information about the directory itself. For example:
```bash
$ ls -l /usr/man
total 12
drwxr-xr-x 2 root root 4096 Apr 10 16:42 man1
drwxr-xr-x 2 root root 4096 Apr 10 16:42 man3
drwxr-xr-x 2 root root 4096 Apr 10 16:42 man7
```

```bash
$ ls -ld /usr/man
drwxr-xr-x 5 root root 4096 Apr 10 16:42 /usr/man
```
# File Type encoding Used by `ls`

| **File Type**         | **Symbol** |
| --------------------- | ---------- |
| Regular file          | -          |
| Directory             | d          |
| Character device file | c          |
| Block device file     | b          |
| Local domain socket   | s          |
| Name pipe             | p          |
| Symbolic link         | l          |
# Regular Files
- Regular files consist of a series of bytes.
- The filesystems impose no structure on their contents.
- Both sequential and random access is allowed.
- Example: Text files, data files, executable programs and shared libraries.
# Directories
- A directory contains named references to other files.
- `mkdir` and `rmdir` is used to create and delete directories respectively.
- The special entries `.` and `..` refer to the directory itself and its parent directory.
- A file's name is stored within its parent directory, not with the file itself. 
- More than one file inside a directory
