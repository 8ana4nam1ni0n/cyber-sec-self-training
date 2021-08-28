# Bandit Level 6

## Goal
The password for the next level is stored somewhere on the server and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

## Solution
First connect through secure shell using `bandit6` as username and the password found in level 5
`ssh bandit6@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

Once inside the server we know that somewhere in the server there is a file that is owned by `bandit7` belongs to the group `bandit6` and has a size of `33 bytes`.

Knowing this info we can use `find` command to look from the root of the server `/` all the files that contains the above mentioned properties as follow:

`find / -user bandit7 -group bandit6 -size 33c -exec cat {} + 2>/dev/null`

Notice that this time we use `-exec cat {} +` flag. What this does is for every file it finds it will substitute the `{}` with the filename found and will run `cat` on it. Also notice the `2>/dev/null` what this does is it will redirect all the stderr output to `/dev/null device` because we dont care about the failures of the command. After running the command we get the password.

password: `HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs`