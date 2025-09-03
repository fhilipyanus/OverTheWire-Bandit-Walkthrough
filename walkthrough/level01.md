# Level 0 -> 1

- Level Page: https://overthewire.org/wargames/bandit/bandit1.html
- Goal: Get the password for the next level by reading the readme file in the bandit0 home directory.
- What you'll learn: understand how to use the cat and ls command
---
Congrats again on getting to level 0! You are now remotely accessing the overthewire server, allowing you to execute commands in their system. The first command we'll discuss is the `ls` command. Type `ls` in the command line and press enter.

The command line will output
```
readme
```

The ls command outputs all files in your current directory. Since the readme file is in your current directory, the command line outputs `readme`. The level page tells us, "The password for the next level is stored in a file called readme." So, we simply need to read this `readme` file. To read a file, use the `cat` command. Type `cat readme` and press enter.

The command line will output something like
```
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

Congrats on getting the password for level 1! All we have to do now is log in to bandit1 using SSH like we did in the previous level. Before we log in, we need to exit bandit0 first. To exit an ssh connection, use the `exit` command. Type `exit` in the command line and press enter.

After your command line is back in your local machine, use ssh to log in to bandit1 just like the previous level.
```
ssh -p 2220 bandit1@bandit.labs.overthewire.org
```
Note: OverTheWire changes their passwords from time to time, so this password might not work for you depending on when you are using it.

The server will prompt you for a password exactly like the last level, simply paste the password and press enter. Congrats, you've entered level 1!
