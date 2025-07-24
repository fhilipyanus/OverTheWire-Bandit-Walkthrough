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

When we enter `cat -`, the command line this we want to enter a flags by design. However, we are not entering a flag in this situation. To reference a file with a hyphen (-) in the name, type `./` before it. The dot (.) references the current directory, and the slash (/) references a path inside the directory. So, all together would be `cat ./-`. We're saying to the command line, "read the file in our current directory with the name -."

You'll get an output that looks like this:
```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

Congrats! You've gotten the password for level2. Just like previous levels, use ssh to login to level 2, then type and enter the password.

```
ssh -p 2220 bandit2@bandit.labs.overthewire.org
```