# Level 8 -> 9

- Level Page: https://overthewire.org/wargames/bandit/bandit9.html
- Goal: Get the password for the next level in the only line of text that occurs only once in the file data.txt 
- What you'll learn: the uniq and sort command.
---

Commands used in this level:
- `uniq`: filters out adjacent duplicate lines.
- `sort`: groups identical lines together by arranging them in order.

The uniq command by default removes adjacent duplicate lines. For example, say we have a file called `file.txt` that contains:

```
apple
apple
orange
orange
lemon
```

The command `uniq file.txt` would output:

```
apple
orange
lemon
```

However, this is not what we want for our level. Our level only wants the unique output, and we achieve this using the `-u` flag. `uniq -u file.txt` would output:

```
lemon
```

Because, only "lemon" is unique in the file. The other lines have duplicates.

However, uniq doesn't work when the duplicates are not together. For example, if `file.txt` were:

```
apple
orange
apple
orange
orange
lemon
```

The command `uniq -u file.txt` would output:
```
apple
orange
apple
lemon
```

This is because the apples and oranges are not sorted together; they are not adjacent. `uniq -u` only checks whether a line is repeated immediately before or after, and not elsewhere in the file. That’s why sorting first is necessary. `sort file.txt` outputs:
```
apple
apple
lemon
orange
orange
orange
```
If we give this standard input to the `uniq -u` command using a pipeline, `sort file.txt | uniq -u`, we get the output:
```
lemon
```
We get the only unique line, even though the original file has lines that are not grouped together.

Let's leave this example, and return to our OverTheWire Level. Let's run `sort data.txt | uniq -u` and see what we get:
```
bandit8@bandit:~$ sort data.txt | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```
You’ll see a long string: that’s the password (yours may be different).

Congratulations, you've gotten the password for level 9. Exit the current connection, and use ssh to login to the server.
```
ssh -p 2220 bandit9@bandit.labs.overthewire.org
```
