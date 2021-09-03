# Bandit Level 19

## Goal
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

## Solution
First connect through secure shell using `bandit19` as username and the password found in level 18
`ssh bandit19@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

This level is pretty straight forward basically you are given a binary that has a setuid set to bandit20 meaning that you can execute commands as bandit20 when using the `bandit20-do` binary.

for example if you run the `id` command you get the following:

`uid=11019(bandit19) gid=11019(bandit19) groups=11019(bandit19)`

as you can see `uid` belongs to `bandit19` and same for gid and groups.

now if you execute the `id` command using the binary we get the following output:

`uid=11019(bandit19) gid=11019(bandit19) euid=11020(bandit20) groups=11019(bandit19)`

as you can see user id group id and groups still belong to `bandit19` but executable id is running as `bandit20`.

In order to read the password from `/etc/bandit_pass/bandit20` we can do  the following:

`./bandit20-do cat /etc/bandit_pass/bandit20` 

this will output the password to next level.


password: `GbKksEFF4yrVs6il55v6gwY5aVje5f0j`