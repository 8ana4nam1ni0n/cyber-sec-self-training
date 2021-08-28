# Bandit Level 3

## Goal
The password for the next level is stored in a hidden file in the inhere directory.

## Solution
First connect through secure shell using `bandit3` as username and the password found in level 2
`ssh bandit3@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

After connecting you type `ls -l` and you will find that there is a directory named `inhere`.

We change directory using the `cd` command. So we do `cd inhere` and change directory to `inhere`.

Inside `inhere` we do `ls -l` but there is nothing there. Now the goal of this problem hints us that there is a hidden file. In order to check for hidden files we can use `-a` flag of the `ls` command as follow:

`ls -a` After running the command we see a file named `.hidden`. Now in order to read this file we can do `cat .hidden` and that will give us the password for next level.


password: `pIwrPrtPN36QITSp3EQaw936yaFoFgAB`