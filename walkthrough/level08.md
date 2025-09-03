# Level 7 -> 8

- Level Page: https://overthewire.org/wargames/bandit/bandit8.html
- Goal: Get the password for the next level in the file data.txt next to the word millionth
- What you'll learn: get more practice with the `grep` command for a better understanding.
---

The password is next to the word millionth in the file data.txt. Do you remember what command we use to look for specific text? Hint: We discussed it in [Level 4 -> 5](/walkthrough/level05.md).

The answer is the `grep` command. In technical terms, the grep command in Linux is a utility used for searching plain-text data sets for lines that match a regular expression or a simple string. The name grep stands for "global regular expression print."

The syntax of the grep command is:
```
grep [options] [pattern] [file...]
```

We don't need to use any options/flags for this problem, so we don't have to type anything for that, the pattern we're looking for is the word "millionth", and the file we want to search is `data.txt`.

So, use the grep command as shown below, and you'll get an output that looks something like this:
```
bandit7@bandit:~$ grep "millionth" data.txt
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
Note: OverTheWire changes their passwords from time to time, so this password might not work for you depending on when you are using it.


Congrats, you got the password for level 8! Use ssh to connect to the server.

```
ssh -p 2220 bandit8@bandit.labs.overthewire.org
```