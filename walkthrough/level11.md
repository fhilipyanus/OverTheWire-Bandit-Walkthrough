# Level 10 -> 11

- Level Page: https://overthewire.org/wargames/bandit/bandit11.html
- Goal: Get the password for the next level stored in the file data.txt, which contains base64 encoded data
- What you'll learn: base64 encoding, the `base64` command, and its `-d` option.
---

Commands used in this level:
- `base64`: used for encoding and decoding data using the Base64 encoding scheme.
- `cat`: used for displaying the contents of files.

Base64 encoding is a process that takes binary data and turns it into text.  For example, imagine you had a communication system that only supports transmission of text, but you want to send someone an image. You can encode the binary data of the image into text using base64, then send the encoded image, then have the receiver decode the base64 text back into an image.

More specifically, Base64 is a way of representing binary data as plain text using only 64 ASCII characters.

In the Linux Command Line, we use the `base64` command to encode or decode. The syntax is as follows:
```
base64 [OPTIONS] [FILE]
```

To get a feel for the problem, let's read `data.txt`.

```
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
```

This is data encoded in base64. What we can do now is decode it using the `base64` command and its `-d` option.
```
bandit10@bandit:~$ base64 -d data.txt
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

Explanation:
- The `-d` flag decodes data.txt.
- If we were to run the `base64` command without `-d`, it would encode instead of decode.
- Question for the reader: If you take the decoded password and run `echo "The password is ..." | base64`, will you get back the original contents of `data.txt`, or a different base64 string? Think about what the input to the encoding step is in each case.

Congrats, you've gotten the password to enter level 11! Use ssh to login to the next level:

```
ssh -p 2220 bandit11@bandit.labs.overthewire.org
```