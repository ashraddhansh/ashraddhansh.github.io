+++
title = "File Conditional Expressions in Bash"
date = 2025-05-04
+++

# What are conditional expressions?
When we use conditional statements like `if` we need to pass some conditions to check whether it's true or not and based on that information we execute some commands.
For example:
```python
i=4
if i>2:
	print("i is greater than 2")
else:
	print("i is lesser than 2")
```

The above program checks that if the value of i is greater than 2 or not if true it prints "i is greater than 2".
The `i>2` is conditional expression.

Likewise bash also have conditional expressions but the syntax is unique.
Conditional expressions in bash are targeted more towards the Linux usability like checking conditions on files, directories etc.

# Conditional Expressions for Files
Here is a example code:

```bash
#! /usr/bin/env bash

filename=./array5.sh

if [[ -a ${filename} ]]; then
  echo "The file exists!"

else
  echo "The file doesn't exists!"

fi

if [[ -d ${filename} ]]; then
  echo "This is a directory!"

else
  echo "This is not a directory!"
fi


if [[ -r ${filename} ]]; then
  echo "The file exists and is readable"

fi


if [[ -s ${filename} ]]; then
  echo "The file exists and file size is greater than zero"

fi

if [[ -w ${filename} ]]; then
  echo "The file exists and file is writable"

fi


if [[ -x ${filename} ]]; then
  echo "The file exists and file is executable"

fi


if [[ -L ${filename} ]]; then
  echo "The file exists and file is symbolic link"
else
  echo "Not a symbolic Link!"
fi
```

In the above code we have multiple `if then` statements that the checking some conditions on file `array5.sh` whole name is stored at the top in the variable name `filename`.

Let's see the first `if then` statement block:

```bash
filename=./array5.sh

if [[ -a ${filename} ]]; then
  echo "The file exists!"

else
  echo "The file doesn't exists!"

fi
```

- Here I have condition `[[ -a ${filename} ]]` for if statement.
- This will check whether the file exists or not in the current directory(because the file path is `./array5.sh`, `.` means the current directory) .
- If the file exists then the program will execute the `then` block and message `The file exists!` will be printed.
- If the file `array5.sh` doesn't exists in the current directory then the program will execute `else` block and message `This file doesn't exists!` will print in the console.
- The ending `fi` is the syntax of the bash `if` statement, it is there to indicate the closing of the `if` block.


There are other conditional expressions for files:

1.  `[[ -d ${filename} ]]` : True if the file is a directory.
2. `[[ -r ${filename} ]]` : True if file exists and readable.
3. `[[ -s ${filename} ]]` : True if file exists and has size larger than zero.(To check empty files)
4. `[[ -w ${filename} ]]` : True if file exists and writable.
5. `[[ -x ${filename} ]]` : True if file exists and executable.
6. `[[ -L ${filename} ]]` : True if file is a symbolic link.

**Note:** The `-x` ,`-w`, `-r` flags check the file permissions for the user that is running the script.
