# Bandit Level 20

## Goal
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think

## Solution
First connect through secure shell using `bandit20` as username and the password found in level 19
`ssh bandit20@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

This is also a stright forward exercise. For this one we have a binary that will connect to a port on localhost. The port number will be passed as argument to the binary.

According to the description in the goal the binary will read a line of text and if that line is equal to the password of the current level then it will send back the password to the next level. In order to make this work we need to listen to a port on localhost using `nc` command and pass the password of the current level as follow:

`echo "<password of current level>" | nc -l localhost -p 55555 &`

> Note: we used the `&` symbol to send the process to the background so that we can keep working in same terminal session.

after running the command we will do the following:

`./suconnect 55555` and we get the following output:

```
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
[1]+  Done                    echo "GbKksEFF4yrVs6il55v6gwY5aVje5f0j" | nc -l localhost -p 55555
```


password: `gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr`