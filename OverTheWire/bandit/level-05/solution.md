# Bandit Level 5

## Goal
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

- human-readable
- 1033 bytes in size
- not executable

## Solution
First connect through secure shell using `bandit5` as username and the password found in level 4
`ssh bandit5@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

After connecting you type `ls -l` and you will find that there is a directory named `inhere` like in level 4.

We change directory using `cd inhere`.

Inside `inhere` we do `ls -l` and we can see there are 20 directories named `maybehere00` all the way to `maybehere19`. Base on the goal we know that there is only 1 file that is human readable, has 1033 size in bytes and is not executable. Since there is too many directories to go 1 by 1 and checking its content we can use the `find` command and give some filters to it to get the file we need as follows: 

`find ./ -readable -size 1033c ! -executable` you can do `man file` to see what each of this flags do.

This will print out the follwing:

`./maybehere07/.file2`

 Now we run `cat ./maybehere07/.file2` and we get the password.

password: `DXjZPULLxYr17uwoI01bNLQbtFemEgo7`