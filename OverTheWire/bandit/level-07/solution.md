# Bandit Level 7

## Goal
The password for the next level is stored in the file data.txt next to the word millionth

## Solution
First connect through secure shell using `bandit7` as username and the password found in level 6
`ssh bandit7@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

After login in we can do `ls -l` and see there as file named `data.txt`. Based on the goal we know that inside there is a word `millionth` and next to that word lies the password of next level.

If we use the `grep` command we can search for the word `millionth` and find our password as follows:

`grep millionth data.txt`

Output:
`millionth	cvX2JJa4CFALtqS87jk27qwqGhBM9plV`

password: `cvX2JJa4CFALtqS87jk27qwqGhBM9plV`