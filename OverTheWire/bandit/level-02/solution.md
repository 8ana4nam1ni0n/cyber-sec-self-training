# Bandit Level 2

## Goal
The password for the next level is stored in a file called `spaces in this filename` located in the home directory

## Solution
First connect through secure shell using `bandit2` as username and the password found in level 1
`ssh bandit2@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

After connecting you type `ls -l` and you will find that there is a single file named `spaces in this filename`. In order to read this file you can either enclose the filename in `""` like this `cat "spaces in this filename"` or you can simply do `cat spaces\ in\ this\ filename` and that should be enough to read the contents of it.


password: `UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK`