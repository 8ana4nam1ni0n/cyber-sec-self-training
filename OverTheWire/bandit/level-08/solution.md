# Bandit Level 8

## Goal
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

## Solution
First connect through secure shell using `bandit8` as username and the password found in level 7
`ssh bandit8@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

Following the goal we know that there is a data.txt file that contains a lot of random passwords but only 1 is unique and thats the one we need. To do this the right way we can sort the data and then use the `uniq` command to see which is the one that is not duplicate and only appears once.

> do `man uniq` to see how it works

to sort the data we can do the follwing:

`sort data.txt` this will give us the following:

```
07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
0efnqHY1ZTNRu4LsDX4D73DsxIQq7RuJ
0efnqHY1ZTNRu4LsDX4D73DsxIQq7RuJ
0efnqHY1ZTNRu4LsDX4D73DsxIQq7RuJ
0efnqHY1ZTNRu4LsDX4D73DsxIQq7RuJ
.
.
.
```

We can see that the sort worked since now all the duplicates are grouped together.

Now we can pipe `|` this result to `uniq -cu` which will give us the following output:

`1 UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR`

The `-c` flags counts the ocurrences of that string in the file and because its unique is only 1. The `-u` command prints only those that dont repeat itself.

> Note: we dont need the -c flag at all I used it just to show that only 1 occurence exists

password: `UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR`