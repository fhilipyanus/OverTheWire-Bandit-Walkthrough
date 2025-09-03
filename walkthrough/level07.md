# Level 6 -> 7

- Level Page: https://overthewire.org/wargames/bandit/bandit7.html
- Goal: Get the password in a file somewhere **in the server**, that is owned by user bandit7, owned by group bandit6, and is 33 bytes in size.
- What you'll learn: what "in the server" means, and the flags -user and -group.
---
In the level [Level 4 -> 5](/walkthrough/level05.md), we've discussed how to use the `find` command to look for specific files. However, we've only discussed using it to look for files in our current directory. To look for a file in the entire server, we use the `/` directory:

```
find /
```

This command will show you every single file in the directory. The root directory / is the top of the filesystem tree, and searching from there searches every directory you have permission to read. We can narrow the search using flags to identify the file that's owned by user bandit7 and group bandit6, and 33 bytes in size.

We've already discussed how to search for specific sizes in [Level 5 -> 6](/walkthrough/level06.md)

```
find / -size 33c
```

Next are the `-user` and `-group` flags. They are used to tell the find command what user and group owns the file.

```
bandit6@bandit:~$ find / -size 33c -user bandit7 -group bandit6
find: ‘/sys/kernel/tracing’: Permission denied
find: ‘/sys/kernel/debug’: Permission denied
find: ‘/sys/fs/pstore’: Permission denied
...
find: ‘/home/bandit27-git’: Permission denied
find: ‘/home/bandit5/inhere’: Permission denied
find: ‘/home/bandit31-git’: Permission denied
```

We're getting a lot of error messages because OverTheWire doesn't give us access to every single server file, only the one necessaary for solving this level. This is normal on real servers too: files and directories have permissions that restrict access to other users. To get rid of the errors, type `2>/dev/null` at the end of the command. `2` refers to error messages, and `/dev/null` refers to a sort of trash can to throw things away. `2>/dev/null` redirects the stderr stream (file descriptor 2) to the “black hole” file `/dev/null`, which discards its contents.

```
bandit6@bandit:~$ find / -size 33c -user bandit7 -group bandit6 2>/dev/null
/var/lib/dpkg/info/bandit7.password
```

Nice, we've got the file. All that's left is to read it.

```
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```
Note: OverTheWire changes their passwords from time to time, so this password might not work for you depending on when you are using it.

Congratulations! You've gotten the password to enter level 7. Use ssh to connect to the server.

```
ssh -p 2220 bandit7@bandit.labs.overthewire.org
```

