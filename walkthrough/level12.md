# Level 11 -> 12

- Level Page: https://overthewire.org/wargames/bandit/bandit12.html
- Goal: Get the password for the next level in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
- What you'll learn: what "rotating" the letters mean, and how to use the `tr` command
---

Commands used in this level:
- `tr`: used for translating or deleting characters from standard input and writing the result to standard output. Its name is short for "translate."
- `cat`: used for displaying the contents of files.

let's read `data.txt`:

```
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
```

We can't read anything. That's because as the level says, all lowercase and uppercase letters have been rotated by 13 positions. What does it mean to rotate the letters? It looks something like this:

Rotated by 1 letter:
1. A -> B
2. B -> C
3. C -> D
4. et cetera

So, if I have the message `Hello`, and I rotated the alphabet by 1 letter, it would become `Ifmmp`. Because `H -> I, e -> f, l -> m, and o -> p`. In short, the entire set of letters `A-Z` is mapped to `B-ZA`. The A is now at the end instead of the front. The same goes for the lowercase letters: `a-z` is mapped to `b-za`. (The process of rotating the alphabet is often called the [Caesar Cipher](https://en.wikipedia.org/wiki/Caesar_cipher). This is a special case of the Caesar cipher, called [ROT13](https://en.wikipedia.org/wiki/ROT13), which rotates letters by exactly 13 positions.)

This rotation is used to encrypt data, or to make sure that people you don't want to read a message can't read the message.

We can automate the rotation using the `tr` linux command. Here is the syntax:

```
tr [OPTION] [SET1] [SET2]
```

Where `SET1` is the original set of characters, and `SET2` is the target set of characters. For example:

```
bandit11@bandit:~$ echo "hello" | tr h j
jello
```

In the example above, the `tr` command changed the letter `h` into `j`.

We can do the same with sets of letters like this:

```
bandit11@bandit:~$ echo "hello" | tr abcdefghijklmnopqrstuvwxyz bcdefghijklmnopqrstuvwxyza
ifmmp
```

or more compactly:

```
bandit11@bandit:~$ echo "hello" | tr a-z b-za
ifmmp
```

We can also include uppercase letters in our set by simply putting the set of lowercase and uppercase letters together (for example, `A-Z` and `a-z` becomes `A-Za-z`):

```
echo "HelLO" | tr A-Za-z B-ZAb-za
IfmMP
```

Now that we've discussed how to use the `tr` command, let's look at the level's problem again. We are asked to turn `data.txt`, which has been rotated by 13 characters, into its original text. If we rotate 13 letters, that means `A -> N, B -> O, C -> P, et cetera`. So, the rotated set is `N-ZA-M` and `n-za-m`. Since we are reverting the rotation, we type the `N-ZA-M` and `n-za-m` as SET1 in the tr command, and type `A-Z` and `a-z` in SET2:

```
bandit11@bandit:~$ cat data.txt | tr N-ZA-Mn-za-m A-Za-z
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

Explanation:
- `cat data.txt` : reads the `data.txt` file
- `|` : gives the output of the `cat` command to the `tr` command
- `tr N-ZA-Mn-za-m A-Za-z` : translates the result of `cat data.txt` from the rotated set of letters into the unrotated set of letters.

However, since there are 26 letters in the alphabet, and we are rotating by 13 letters, the order of SET1 and SET2 coincidentally doesn't matter:

```
bandit11@bandit:~$ cat data.txt | tr A-Za-z N-ZA-Mn-za-m
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

Congrats, you've gotten the password to enter level 12! Use ssh to login to the next level:

```
ssh -p 2220 bandit12@bandit.labs.overthewire.org
```