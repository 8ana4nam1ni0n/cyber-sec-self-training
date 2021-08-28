# Bandit Level 1

## Goal
The password for the next level is stored in a file called `-` located in the home directory

## Solution
First connect through secure shell using `bandit1` as username and the password found in level 0
`ssh bandit1@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

You will find a file with `-` being the filename. This is a bit tricky because if you type `cat -` the shell will keep waiting for an optional flag. In unix optional flags by convention are `<command> -<flag> args` so in order to let the shell know that you are not specifying a flag but a filename you will need to provide the full path of the file or simply feed `-` contents using `<` input redirection operator to `cat` command as follows:

`cat < -`

> Note: There are many ways to achieve the same result. I just chose the simplest for me.

password: `CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9`