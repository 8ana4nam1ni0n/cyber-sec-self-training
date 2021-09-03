# Bandit Level 14

## Goal
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

## Solution
First connect through secure shell using `bandit14` as username and the password found in level 13
`ssh bandit14@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

This exercise is a very straight forward one. Basically once we log in into `bandit14` we need to resubmit the password to port `30000` of `localhost`

This can be achieve easily with `nc` command. To do this we do the followin:

`echo "<password this level>" | nc localhost 30000`

This will replay to us the password to next level.


password: `BfMYroe26WYalil77FoDi9qh59eK5xNr`