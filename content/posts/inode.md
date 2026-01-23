+++
title = "Inode(Index Node)"
date = 2025-03-05
+++

- Inode is a date structure.
- It stores the metadata and other information of files except the file name.
- Each file and [Directory](@/posts/directory.md) has its own unique inode.
# Type of Info stored in Inode
## Metadata
- File type
- File permissions
- Owner and Group ID(UID & GID)
- File size
- Timestamps (birth, access, modification, change times)
- Number of [Hard link](@/posts/hard-link.md) & [Soft Link (Symbolic Link)](@/posts/soft-link.md)
## Location of Data blocks
Pointers of the disk blocks where data is stored.

_the file name and the directory path is not stored in inode these info are managed separately in [[Directory Entry]] that map file names to inode numbers._
# Working of Inode
- Each file and directory has its inode.
- When new file or directory is created the file-system assigns a unused inode to it.
- It serves as identifier for file and directory.

# Viewing Inode
```bash
ls -i
```
# Creation of inodes
- When a file system is created a fixed number of inodes are pre-allocated based on the size of file-system.
- The number of inodes are in the ratio with the file system size. (like 1 inode per 16KB).
# Dynamic assignment of inodes
- When new file or directory is created the file-system looks for first available unallocated inode from the inode table and assign it.
- inode number can be reused, when file or directories are deleted the inode of those are marked unallocated by the file-system and then can be reused.
