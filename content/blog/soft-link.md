+++
title = "Soft Link(Symbolic Link)"
date = 2019-11-27
+++
- Soft links(symbolic links) are specific files that points to the **path** of another file or directory.
- Acts as a shortcut of the original file. 
- Soft links don't share the same inode or file data, they act as shortcut or reference to another file.
- Each soft link has it's own inode.
- The original file inode points to the actual data block in the disk space while the inode of the soft-link file points to the path of the original file.
- So when we delete the original file the inode of that file is reclaimed by inode table. 
- The reason why soft-link files are inaccessible after original file deleted is because the inode of main file doesn't points to the disk space anymore, after that the inode of soft link can't fetch that location of the original file of the file system.

![image](/images/soft-link.png)
