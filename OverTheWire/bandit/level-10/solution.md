# Bandit Level 10

## Goal
The password for the next level is stored in the file data.txt, which contains base64 encoded data

## Solution
First connect through secure shell using `bandit10` as username and the password found in level 9
`ssh bandit10@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

For this exercise we have a file `data.txt` that is `base64` encoded. Luckily we have a `base64` command under our sleeves. 

> Note: `man base64` will tell you how to use this command.

if we run `cat data.txt` we get the follwing output:

`VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==`

That is how a base64 encoded string looks like. To decode this all we need is to run the following command:

`base64 -d data.txt` 

Output:

`The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR`

password: `IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR`