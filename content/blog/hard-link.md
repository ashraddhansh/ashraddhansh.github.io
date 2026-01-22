+++
title = "Hard Link"
date = 2019-11-27
+++
- Hard link is a directory entry that maps the file name with an inode in a file-system.
- A hard link creates a additional name for the same file, pointing at the same inode thus referring the same data.
- Hard links are indistinguishable from the original file even the timestamps will be the same(access time, modify time etc).
- Each file must have atleast one hard link because the hard link maps the file name with its inode which contains the metadata and pointers to the file content.
- Hard links can't be created between different file systems or partitions.
# Creation of Hard links
```bash
touch hello.txt
ln hello.txt world.txt
```

- Here the `world.txt` is the hard link to `hello.txt`, they both are pointing to the same inode number thus the same data.
- Both files now contains the same data changes done to one will reflect in other file.
- Deleting one doesn't affect the other.
