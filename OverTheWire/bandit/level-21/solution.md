# Bandit Level 21

## Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Try connecting to your own network daemon to see if it works as you think

## Solution
First connect through secure shell using `bandit21` as username and the password found in level 20
`ssh bandit21@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

For this exercise all we need to do is check the `/etc/cron.d/cronjob_bandit22` file as specified in the description in the Goal section.

For this we run the following command:

`cat /etc/cron.d/cronjob_bandit22`

Output: 
```
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

The output tells us that on machine startup a script found in /usr/bin/cronjob_bandit22.sh will run in the background. 

So in order to get the password we can read the contents of the script and see what it does as follow:

`cat /usr/bin/cronjob_bandit22.sh`

Output:
```bash
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

we can see that the script reads the password and stores it into `/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`

if we read the contents of the file we get the password to next level

`cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`

password: `Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI`