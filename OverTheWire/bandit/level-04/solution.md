# Bandit Level 4

## Goal
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

## Solution
First connect through secure shell using `bandit4` as username and the password found in level 3
`ssh bandit4@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

After connecting you type `ls -l` and you will find that there is a directory named `inhere` like in level 3.

We change directory using `cd inhere`.

Inside `inhere` we do `ls -l` and we can see there are 10 files named `-file00` all the way to `-file09`. Base on the goal we know that there is only 1 file that is human readable. To check this since all files have the same name but the last digits are what makes them different we can use a wildcard along with the `file` command as follows:

`file ./-file*` where `*` is the wildcard.

This will list all the files with its file type looking something like this:

```
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```
 Looking at the result we can assume that `-file07` is the one with the password for next level.

 We run `cat < -file07` and we get the password.

password: `koReBOKuIDDepwhWk7jZC0RTdopnAYKh`