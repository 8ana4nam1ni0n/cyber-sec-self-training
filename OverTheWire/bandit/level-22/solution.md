# Bandit Level 22

## Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

## Solution
First connect through secure shell using `bandit22` as username and the password found in level 21
`ssh bandit22@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

For this exercise all we need to do is check the `/etc/cron.d/` file as specified in the description in the Goal section.

For this we run the following command:

`ls /etc/cron.d/`

Output: 
```
cronjob_bandit15_root  cronjob_bandit17_root  cronjob_bandit22       cronjob_bandit23       cronjob_bandit24       cronjob_bandit25_root  .placeholder
```

We can see there is a `cronjob_bandit23`. We inspect it by down the following:

`cat /etc/cron.d/cronjon_23`

Output:
```
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```
We see that this cronjob executes `cronjob_bandit23.sh` when the machine starts up.

We inspect the contents of this script as follow:

`cat /usr/bin/cronjob_bandit23.sh`

Ouput:
```bash
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

This is an interesting script but basically what it does is that it echoes the string `"I am user bandit23"` then it sends the output of the echo to `md5sum` which will calculates the md5 hash of it and then uses the cut command to delimit the output by spaces and finally grabs the first field which is the actual md5 hash. after this it copies the contents of `/etc/bandit_pass/bandit23` into `/tmp/<md5sum calculated>`

so if we run the same command  we get the following:

```bash
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
# output:
8ca319486bfbbc3663ea0fbe81326349
```

With that hash we do the following:

`cat /tmp/8ca319486bfbbc3663ea0fbe81326349`

Output:
`jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n`

password: `jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n`

