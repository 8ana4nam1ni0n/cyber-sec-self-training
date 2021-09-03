# Bandit Level 17

## Goal
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

## Solution
First connect through secure shell using `bandit17` as username and the credential found in level 16
`ssh  -i <private key found> bandit17@bandit.labs.overthewire.org -p 2220`

> Note: If you get an error that the key has too many privileges you need to change it using 
>
> `chmod 400 <private key file found>`

For this level we need to find the difference between `passwords.old` and `passwords.new` files. According the hint in Goal only 1 line is different. For this we will use the `diff` command as follow:

`diff passwords.old passwords.new`

Output:

```
42c42
< w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii
---
> kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
```

The first line containing the `<` symbol is the old password and the one with `>` symbold is the new password and the one we need for next level.

password: `kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd`