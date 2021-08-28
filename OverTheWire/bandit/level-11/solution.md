# Bandit Level 11

## Goal
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

## Solution
First connect through secure shell using `bandit11` as username and the password found in level 10
`ssh bandit11@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

In this exercises we get that all letters inside `data.txt` files has been rotated 13 times. This is a very known encoding known as `rot13`.

> Note: Look for Rot13 in google to see how it works

For this there is a command in linux we can use to substitute letters in a file. This command is known as `tr`

The way this command works is that you specified a set of rules on how to substitute and then feed it with a file or string and it will perform the substitution for you.

So to solve this problem we run the following command:

`tr A-Za-z N-ZA-Mn-za-m < data.txt`

> Note: `man tr` to learn how to use this command

Output:
`The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu`

password: `5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu`