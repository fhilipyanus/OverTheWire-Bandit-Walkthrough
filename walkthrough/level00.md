# Level 0 - Bandit
Level Page: https://overthewire.org/wargames/bandit/bandit0.html
Goal: Log into the game using SSH.
What you'll learn: understand how to use the ssh command
---
To connect to the bandit wargame server, or any other remote access task, we use the ssh command. Here is the syntax of the ssh command:
```
ssh -p <port> user@hostname
```
In the level page, it is mentioned that:
- The host to which you need to connect is bandit.labs.overthewire.org
- on port 2220
- The username is bandit0

So, to connect to the ssh server, simply enter the command as such:
```
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

The server will then prompt you for a password. 
![server asking for password](/assets/level00img1.jpg)



