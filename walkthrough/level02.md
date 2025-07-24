# Level 1 -> 2

- Level Page: https://overthewire.org/wargames/bandit/bandit2.html
- Goal: Get the password for the next level by reading a file called - in the bandit1 home directory.
- What you'll learn: how to read files with names like "-" and why it's a complication.
---
Your command line is now in the home directory of bandit1. If we type and enter the `ls` command, we'll see:
```
-
```

There is a file in our current directory with the name "-". The password is in this file. Let's try to use the command as we did in the previous level. `cat -` and the command line outputs:
```
bandit1@bandit:~$ cat -

```
It outputs nothing. Instead, it is asking for input. This is because of the way linux commands work. They have modifiers that modify the behavior of a command or provide additional instruction, and we call them flags/options/switches. They are typically appended to a command and begin with a hyphen (-) for short flags (e.g., -a) or a double hyphen (--) for long flags (e.g., --all).

To exit input mode, press the shortcut Ctrl+C.

When we enter `cat -`, the command line thinks we are using the hyphen (-) to refer to standard input. It is a common convention for a hyphen (-) to refer to standard input. This makes things confusing, because that's not what we want to refer to. Instead, we want to refer to the file with the name "-". To solve this, we use `./` before the filename. The dot (.) refers to the current directory, and the slash (/) seperates paths in our command. So, all together would be `cat ./-`, this tells the system: “Look in the current directory for a file named - and display its contents.”

Your command line will look something like this:
```
bandit1@bandit:~$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

Congrats! You've gotten the password for level2. Just like previous levels, exit the current connection, use ssh to login to level 2, then type and enter the password.

```
ssh -p 2220 bandit2@bandit.labs.overthewire.org
```