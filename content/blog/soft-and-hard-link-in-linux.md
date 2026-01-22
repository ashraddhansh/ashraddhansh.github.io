+++
title = "Soft and Hard Links in Linux"
date = 2025-05-05
+++

# Links in Linux Filesystem
- A link is a mechanism that allows multiple references (names or path) to point at single file or directory within the filesystem.
- It is essentially a way to create alternate access points to data that already exists in the disk, either by referencing the actual data or by referencing the file's path.

So in short:
> In the Linux filesystem, **links** are references to files or directories. 

# Inode(Index-node)
Before understanding more about links first we need to understand about inode.
- Inode is a data structure.
- It is used to store metadata about the files and directories.
- An inode is a unique identifier for a file within a specific filesystem.
- Each file and directory has it's own unique inode number.(except hard links)
- It can be accessed by using `-i` flag in `ls` command.

```bash
$ ls -i
6685071 Clone  6834739 Desktop    6708661 Documents  6707926 Music     6837431 packettracer  7112736 Projects  6708639 Scripts  6834960 Templates  6708514 Wallpaper
8394325 data   6708934 Developer  6707119 Downloads  6708058 Obsidian  6704479 Pictures      6834961 Public    6708492 temp     6708587 Videos
```

Here you can see the inode numbers of directories in my home directory.
# Types of Links
There are two types of links:
1. Hard Link
2. Soft Link(Symbolic Link)
# Hard Link
- Let's say I have a file named `file1.txt` and I created a hard link of `file1.txt` as `file2.txt` which is essentially a reference to the `file1.txt`. 

![image](/images/soft-and-hard-links-in-linux-1.png)
- As it appears to be that there are two files here but actually in disk the content of the file is stored only once and both files points to that memory location
- So now when I try to access any of two files the filesystem point to the highlighted disk space.
- Both files will have same inode numbers because inode numbers are allotted according to disk space, as both files points to the same disk address they will have the same inode number.
- When you delete any one of the file the other one will be unaffected, but when you make changes in one file, it will reflect in the other file, because at the low level you are manipulating the bits stored in the disk address which is linked to both files.
## Creating Hard Link
Let's create a file and populate it with some text.
```bash
touch hello.txt
echo "hello, world" >> hello.txt
```

Now let's create a hard link of `hello.txt` to `hello2.txt`
```bash
ln hello.txt hello2.txt
```

Now check the contents of the `hello2.txt`
```bash
$ cat hello2.txt 
hello, world
```

It is same as of `hello.txt`.

Now let's see the inodes of these files, they are same it means both files points to the same location in the disk.
```bash
$ ls -i
9708270 hello2.txt  9708270 hello.txt
```

Try to make changes in one file and then see if the changes reflect in other file. Delete one file and see if it affects the other file.
The advantage of hard link is it provides file redundancy without data duplication.
# Soft Link(Symbolic Link)
- In soft link the linked file points to the file not the disk location.
- The `file2.txt` contains the pathname of `file1.txt`. 
- Unlike hard links, a symlink doesn't point directory to the files's inode.

![image](/images/soft-and-hard-links-in-linux-2.png)
- Let's create a file and populate it
```bash
touch test1.txt
echo "this is test1 file" >> test1.txt 
```

- Now create a symbolic link
```bash
ln -s test1.txt test2.txt
```

- Let's see the inode of these files. They are different because they are not pointing to the same disk address. The file `test2.txt` actually contains a string that holds the path of the `test1.txt` not the contents of the target file.
```bash
ls -i
9708272 test1.txt  9708274 test2.txt
```

- in this case also the changes of one file will reflect on other file also.
- If you delete the `test1.txt` then `test2.txt` will be useless. But vice-versa will not be true.
# Advantage of Symbolic Link over Hard Link
1. Can link to directories.
2. A soft link can point to a file or directory **on a different mounted filesystem**, partition, or device. Hard link can't link files between different devices or filesystem because hard links point directly to inodes, and inodes are only meaningful within the filesystem where they were created.
3. Can link to non-existent targets. Useful in scripting, where the target might appear later.
4. Dynamic path resolution. Symbolic links resolve to the **current location of the target path**. If the symlink is updated (e.g., re-pointed to a different version of a file), it reflects the change immediately. Useful for switching between different versions of software.
