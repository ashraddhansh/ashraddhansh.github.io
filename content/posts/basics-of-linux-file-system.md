+++
title = "Basics of Linux File System"
date = 2025-03-05
+++

# Directory
- It is a special type of file in a Linux file-system.
- It acts as a container for other files and directories.
- The content stored in a directory is essentially a list of [Directory Entry](@/posts/directory-entry.md).
- These are organized in hierarchical structure.
- In Linux everything is a file.
# Directory Entry
- It is a record in a directory.
- It associates or maps a file name(human readable) with its inode number in a file-system.
- A directory entry contains the file name and pointer to the file's inode.
- It is stored in [Directory](@/posts/directory.md).
- It doesn't store the file metadata that is done by [Inode(Index Node)](@/posts/inode.md)

# Inode(Index Node)
- Inode is a date structure.
- It stores the metadata and other information of files except the file name.
- Each file and [Directory](@/posts/directory.md) has its own unique inode.
## Type of Info stored in Inode
### 1. Metadata
- File type
- File permissions
- Owner and Group ID(UID & GID)
- File size
- Timestamps (birth, access, modification, change times)
- Number of [Hard link](@/posts/hard-link.md) & [Soft Link (Symbolic Link)](@/posts/soft-link.md).
### 2. Location of Data blocks
Pointers of the disk blocks where data is stored.

_the file name and the directory path is not stored in inode these info are managed separately by [Directory Entry](@/posts/directory-entry.md) that map file names to inode numbers._
## Working of Inode
- Each file and directory has its inode.
- When new file or directory is created the file-system assigns a unused inode to it.
- It serves as identifier for file and directory.

## Viewing Inode
```bash
ls -i

output ->
4073139 bubble  4073136 bubble.c  4073141 bubble.png  4073138 insertion  4073137 insertion.c
```

This will return the file names with it's inode numbers.
## Creation of inodes
- When a file system is created a fixed number of inodes are pre-allocated based on the size of file-system.
- The number of inodes are in the ratio with the file system size. (like 1 inode per 16KB).
## Dynamic assignment of inodes
- When new file or directory is created the file-system looks for first available unallocated inode from the inode table and assign it.
- inode number can be reused, when file or directories are deleted the inode of those are marked unallocated by the file-system and then can be reused.
# Hard link
- Hard link is a directory entry that maps the file name with an inode in a file-system.
- A hard link creates a additional name for the same file, pointing at the same inode thus referring the same data.
- Hard links are indistinguishable from the original file even the timestamps will be the same(access time, modify time etc).
- Each file must have atleast one hard link because the hard link maps the file name with its inode which contains the metadata and pointers to the file content.
- Hard links can't be created between different file systems or partitions.
## Creating a hard link
```bash
touch hello.txt
ln hello.txt world.txt
```

- Here the `world.txt` is the hard link to `hello.txt`, they both are pointing to the same inode number thus the same data.
- Both files now contains the same data changes done to one will reflect in other file.
- Deleting one doesn't affect the other.
