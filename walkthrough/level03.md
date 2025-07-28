# Level 2 -> 3

- Level Page: https://overthewire.org/wargames/bandit/bandit3.html
- Goal: Get the password for the next level by reading a file with spaces in the name in the bandit2 home directory.
- What you'll learn: how to read files with spaces in the name and why it's a complication.
---
Your command line is now in the home directory of bandit2. If we type and enter the `ls` command, we'll see:
```
spaces in this filename
```

There is a file named `spaces in this filename` in our current directory. The password is in this file. Let's try to use the cat command as we did in the previous level. `cat spaces in this filename` and the command line outputs:
```
bandit2@bandit:~$ cat spaces in this filename
cat: spaces: No such file or directory
cat: in: No such file or directory
cat: this: No such file or directory
cat: filename: No such file or directory
```
Instead of reading the file "spaces in this filename", the cat command tries to read the files "spaces", "in", "this", and "filename". It fails and says "No such file or directory" because there is no file with those individual names. The shell doesn't know that you're trying to refer to one file, instead it thinks you're referring to four files. So how do you read a file that has spaces in its name?

Wrap the filename in double-quotes like this:
```
cat "spaces in this filename"
```

Your command line will look something like this:
```
bandit2@bandit:~$ cat "spaces in this filename"
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

The shell parses and splits arguments before the `cat` command even runs. Using quotes is how you prevent word splitting and group words into a single argument. Later you'll encounter filenames with other special characters like *, &, and #, and quotation marks will be your friends.

Experiment: Try it with single quotes, what happens?
```
cat 'spaces in this filename'
```
What if you use _backslashes_ instead of quotes like this?
```
cat spaces\ in\ this\ filename
```

Congrats! You've gotten the password for level 3. Just like previous levels, exit the current connection, use ssh to login to level 3, then type and enter the password. The **Key Takewawy** is that in the shell, spaces are used to separate command arguments. If a filename contains spaces, you need to group it with quotes or escape characters to ensure it's interpreted correctly.


```
ssh -p 2220 bandit3@bandit.labs.overthewire.org
```