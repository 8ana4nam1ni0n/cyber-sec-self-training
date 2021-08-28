# Bandit Level 9

## Goal
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

## Solution
First connect through secure shell using `bandit9` as username and the password found in level 8
`ssh bandit9@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

For this exercise we are given a binary file and we are told that the password is stored in on of the few human-readable strings preceded by several `=` characters.

We know the `grep` command but it won't work against binary files. For this we need the help of another command called `strings`. This command will output all the human readable strings within a file. Now using `strings` command along with grep we can achieve the following:

`strings data.txt | grep -E "=+"`

Output:
```
========== the*2i"4
========== password
Z)========== is
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```
As you can see we have password looking like string in which is the answer we are looking for.

password: `truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk`