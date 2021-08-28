# Bandit Level 0

## Goal
The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

## Solution
First connect through secure shell using the provided username, password, hostname and port as follows:
`ssh bandit0@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

Once in the machine type `ls` command to see whats in the directory. There will be a `readme` file. Use `cat readme` to read the contents of the file and there will be the password for level 1.

password: `boJ9jbbUNNfktd78OOpsqOltutMc3MY1`