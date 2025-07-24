# Level 1

- Level Page: https://overthewire.org/wargames/bandit/bandit0.html
- Goal: Log into the game using SSH.
- What you'll learn: understand how to use the ssh command
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

The level page tells us that the password is **bandit0**, so type that and send it to the server. However, the way OverTheWire levels are set up, is that they hide the password when you type it for confidentiality. You will not see what you type, but you did type it down. Once you type bandit0, press enter.

Congrats! you are now in level 0.



