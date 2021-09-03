# Bandit Level 18

## Goal
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

## Solution
First connect through secure shell using `bandit18` as username and the password found in level 17
`ssh bandit18@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

In this level as soon as you log in you get kicked out from the server. According to the hint all we know is that the password is located on a file named `readme` on the home directory. Luckily for us the ssh command allows us to execute a command after connection as follow:

To send a file to remote:
`cat file_to_send | ssh <user>@<domain>`

To receive a file from remote:
`ssh <user>@<domain> cat file_from_remote`

For this exercise we just need the latter so we do the following:

`ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme`

Output:

```
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password:
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```

as you can see we got the password displayed by the `cat` command before disconnecting from the session.


password: `IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x`