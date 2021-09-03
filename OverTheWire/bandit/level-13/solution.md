# Bandit Level 13

## Goal
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

## Solution
First connect through secure shell using `bandit13` as username and the password found in level 12
`ssh bandit13@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

In this exercise we won't find a password for the next level but we need to ssh into the next level using a private key found in the home directory of the bandit13 machine.

To make this happen after reading the man pages of `ssh` command we found that the `-i` flag can be use to specify a login with a key file, in our case the `ssh.private` file.

Since we are already in the `bandit.labs.overthewire.org` machines we can substitute that with `localhost` following the advise given in the Goal section.

To log in into the bandit14 machine we do the following:

`ssh -i ssh.private bandit14@localhost`

This will log in into the bandit14 machine.. once in there we do

`cat /etc/bandit_pass/bandit14` and we get the password for next level.

password: `4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e`