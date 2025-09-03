# Level 4 -> 5

- Level Page: https://overthewire.org/wargames/bandit/bandit5.html
- Goal: Get the password for the next level by reading the only human readable file in the `inhere` directory.
- What you'll learn: how to find files, identify their type, and filter them out.
---
Your command line is now in the home directory of bandit4. The level page tells us that the password for the next level is stored in the only human-readable file in the inhere directory. Let's understand what this means.

What is a human-readable file? A human-readable file is typically plain text: something you can open in a text editor and make sense of. A human-readable file might look something like: "afjbnawe289w." A non human-readable file might look something like: ֨,9KL��+ӑ�'��,�BtZ�@P0N��Q��.

Now, let's check out the inhere directory to see what we're working with.
```
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```

There are 10 files, which is too many to check each file manually. So, we'll speed things up using the `find` command, `file` command, and `grep` command.

The `find` command is used to search for files and directories.
The `file` command is used to identify the type of files.
The `grep` command is used to filter things.

Here's how we're going to automate looking for the human-readable files:
1. find all files in the inhere directory
2. identify the file type of the files
3. filter out the files that aren't text (human-readable), so we are left with only the text file.

Here's all of it put together:
```
find . | xargs file | grep text
```

The | symbol is called a pipeline. It's used for chaining commands together. To see how this command works, let's execute it step by step.

```
bandit4@bandit:~/inhere$ find .
.
./-file01
./-file09
./-file05
./-file02
./-file03
./-file06
./-file07
./-file08
./-file04
./-file00
```
`find .` means find all files in this directory.

```
bandit4@bandit:~/inhere$ find . | xargs
. ./-file01 ./-file09 ./-file05 ./-file02 ./-file03 ./-file06 ./-file07 ./-file08 ./-file04 ./-file00
```
`xargs` changes the formatting of the output.

```
bandit4@bandit:~/inhere$ find . | xargs file
.:         directory
./-file01: data
./-file09: data
./-file05: data
./-file02: data
./-file03: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file04: data
./-file00: data
```
`file` shows us the types of each file. Note: we used xargs because the `file` command expects the files to be written in one line. `xargs` does that for us. `xargs` is commonly used after pipelines as a reformatter for commands that demand specific formats. Note: `xargs` alone can sometimes cause problems. It works here because the filenames are simple, but in real-world cases with spaces or special characters, it's safer to use `find . -print0 | xargs -0 file` to avoid parsing issues. `-print0` tells `find` to print file names separated by a null byte instead of a newline. `-0` tells xargs to expect null-terminated input instead of newline-terminated.

Question for extra understanding: The file command labels file types heuristically. It’ll say ‘ASCII text’ if the file consists only of readable characters. This works for most human-readable content, but not all. What do you think would happen if the file were in UTF-8 or had special characters?

```
bandit4@bandit:~/inhere$ find . | xargs file | grep text
./-file07: ASCII text
```
`grep text` filters out every line that doesn't have the word "text" in it, leaving us with the only human-readable file. 


Now, all that's left is to read the file (Remember, the file name `-file07` starts with `-`, which means we need to read it by typing `./` before the name as we discussed in [level 1 -> 2](/walkthrough/level02.md):
```
bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```
Note: OverTheWire changes their passwords from time to time, so this password might not work for you depending on when you are using it.

Congratulations on getting the password for level 5! Just like previous levels, exit the current connection, use ssh to login to level 5, then type and enter the password.

```
ssh -p 2220 bandit5@bandit.labs.overthewire.org
```
