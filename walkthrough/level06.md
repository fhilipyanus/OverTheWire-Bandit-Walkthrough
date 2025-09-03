# Level 5 -> 6

- Level Page: https://overthewire.org/wargames/bandit/bandit6.html
- Goal: Get the password in a file somewhere under the inhere directory, that is human-readable, 1033 bytes in size, and not executable.
- What you'll learn: the flags -size and -executable in the find command, and also how to implement a logical NOT in commands.
---
In the previous level [Level 4 -> 5](/walkthrough/level05.md), we've discussed how to scan for human-readable files in a directory like this:
```
bandit5@bandit:~$ find . -print0 | xargs -0 file | grep text
./.profile:                        ASCII text
./.bashrc:                         ASCII text
./inhere/maybehere14/-file2:       ASCII text, with very long lines (8350)
./inhere/maybehere14/-file1:       ASCII text, with very long lines (4281)
...
./inhere/maybehere08/.file2:       ASCII text, with very long lines (746)
./inhere/maybehere08/.file1:       ASCII text, with very long lines (8168)
./inhere/maybehere08/spaces file1: ASCII text
./.bash_logout:                    ASCII text
```

Note: We’re still using `-print0` and `-0` so that filenames with spaces or special characters are handled safely.

There are a lot of ASCII text files in this level. How do we identify which file is 1033 bytes in size and not executable? We use the `-size` and `-executable` flags in the find command.

```
find . -size 1033c -print0 | xargs -0 file | grep text
```

`-size 1033c` means exactly 1033 bytes, the `c` tells `find` to count in bytes instead of 512-byte blocks.

```
find . ! -executable -print0 | xargs -0 file | grep text
```

`-executable` tells the find command to look for executable files. Meanwhile, `! -executable` tells find to look for files that aren't executable. In find, `!` (or `-not`) negates the condition that follows; here it inverts `-executable` so we only match non-executable files.

Altogether, the command looks like this:

```
bandit5@bandit:~$ find . -size 1033c ! -executable -print0 | xargs -0 file | grep text
./inhere/maybehere07/.file2: ASCII text, with very long lines (1000)
```

We've got our file, all we have to do now is read it.

```
bandit5@bandit:~$ cat ./inhere/maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```
Note: OverTheWire changes their passwords from time to time, so this password might not work for you depending on when you are using it.

Congratulations! You've gotten the password to enter level 6. Use ssh to connect to the server.

```
ssh -p 2220 bandit6@bandit.labs.overthewire.org
```

