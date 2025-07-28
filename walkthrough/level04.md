# Level 3 -> 4

- Level Page: https://overthewire.org/wargames/bandit/bandit4.html
- Goal: Get the password for the next level by reading a hidden file in the `inhere` directory.
- What you'll learn: how to change directories, and look for and read hidden files.
---
Your command line is now in the home directory of bandit3. If we type and enter the `ls` command, we'll see:
```
bandit3@bandit:~$ ls
inhere
```

There is a directory called `inhere`. A directory is a container for organizing data.

To enter the `inhere` directory, or open the folder, we use the `cd` command like so:
```
cd inhere
```

After entering this command, you'll notice that the terminal's words have changed from `bandit3@bandit:~$` to `bandit3@bandit:~/inhere$`. This means we are now inside the `inhere` directory.

The level page tells us there is a file in this directory, but when we run the `ls` command:
```
bandit3@bandit:~/inhere$ ls
```
Nothing pops up. That's because the file we're looking for is a _hidden_ file. To look for hidden files, the `ls` command alone can't do it, it needs a flag, which is basically an option in a command.  Flags are characters or words, typically preceded by a hyphen (-) or double-hyphen (--), that are passed to a command to alter its behavior or output. (Note: Sometimes flags are also called options, switches, or modifier.)

To look for hidden files using `ls`, we use the `--all` flag. A flag is like a remote control setting. The ls command is the TV, and the `--all` flag is like pressing the “show all channels” button; it lets you see the hidden channels too.
```
bandit3@bandit:~/inhere$ ls --all
.  ..  ...Hiding-From-You
```

`-a` also works; it is a shortened version of `--all`
```
bandit3@bandit:~/inhere$ ls -a
.  ..  ...Hiding-From-You
```

As you can see, there is a file named `...Hiding-From-You` in our current directory. Filenames starting with a . are hidden. All we have to do now is read it, using `cat` like this:
```
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

However, what are `.` and `..` in the output of `ls -a` before our filename? Those are entries to directories. They are technically required to make directories navigable. They aren’t regular files or folders; they’re shortcuts: `.` points to the current folder, and `..` points to the folder that contains this one. They are usually hidden, but since we used `ls --all`, which shows all files, the `.` and `..` files are also shown.

Congrats on getting the password for level 4! The **Key Takeaway** here is that the `ls` command alone doesn't show hidden files, and it needs the `--all` or `-a` flag to do so. Just like previous levels, exit the current connection, use ssh to login to level 4, then type and enter the password.

```
ssh -p 2220 bandit3@bandit.labs.overthewire.org
```