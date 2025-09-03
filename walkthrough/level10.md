# Level 9 -> 10

- Level Page: https://overthewire.org/wargames/bandit/bandit10.html
- Goal: Get the password for the next level stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.
- What you'll learn: the strings command.
---

Commands used in this level:
- `strings`: used to extract printable character sequences (strings) from binary files.
- `grep`: used for searching plain-text data sets for lines that match a regular expression or a simple pattern.

If we read `data.txt` with the command `cat data.txt`, you'll find that almost everything is pretty much unreadable. Here's a snippet of the output:
```
l����y{�9������=�b�Q�����[��7�:����6�R�2ˈ�$�Ȫ'�����ppH�@}��F�½��QՉ�]�ý����b����E�O��*j�#�4�h��P[
       ��D�#��=
               ��_⟳�ʰ�$��]S�Ϟ��:���[Gm�qs����m�	��c
�␦���t��g���~����ڼ?as�cl�g�K#��F��$*�;��#��V��*��Z;�u��v*���e}��v�c
U6���o�x�V]�!�Xq�є��S�y�������m
c�"��l>IF<¨"��ʋM���GHof/;��␦)
```

Your output may look different depending on encoding, but the important point is that it’s mostly unreadable binary.

The command that extracts strings out of a file is the `strings` command. The syntax of the strings command is:
```
strings [options] filename(s)
```

In the CLI, the output will look something like this:

```
bandit9@bandit:~$ strings data.txt
tvFJ
*M'Jg
>Id#{
VN5ZTH
9~T4
LkoV
$.`[
>K3Z
6tO/
PCa/
Z56Tn
...
```

The command outputs all strings in the file. How do we look for the lines preceded by several "=" characters? We pipeline the output of `strings` into `grep` as shown below:

```
bandit9@bandit:~$ strings data.txt | grep "=="
========== theg
========== password
========== is
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

Explanation:
- the `strings` command gives all the strings in data.txt
- the `grep` command filters out all lines of strings from the strings command that don't have "==" in them.
- Analogy: `strings` is like sifting gravel to get pebbles, and `grep` is like picking only the shiny ones

If we put the words together, it obviously says:

```
the password is FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```
Note: OverTheWire changes their passwords from time to time, so this password might not work for you depending on when you are using it.

Congrats, you've gotten the password to enter level10! Use ssh to login to the next level:

```
ssh -p 2220 bandit10@bandit.labs.overthewire.org
```

