# Bandit Level 12

## Goal
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

## Solution
First connect through secure shell using `bandit12` as username and the password found in level 11
`ssh bandit12@bandit.labs.overthewire.org -p 2220`

Enter password when prompted.

For this exercise we are given a hex dump inside `data.txt` and we know based on the goal that the file is heavily compressed.

First we create a dir to work in in `/tmp` directory as advised in the goal as follows:

`mkdir /tmp/8ana4nam1ni0n`

Then we change to the created directory as follows:
`cd /tmp/8ana4nam1ni0n`

Then we copy the `data.txt` into our new directory
`cp ~/data.txt .`

Now back to work

To revert the hex dump back to a binary we can use the `xxd` command as follows:

`xxd -r data.txt > data1`

if we do `file data1` we can see that is gzip file. Since the exercise says this was heavily compressed we can assume that it was compressed multiple times. Now when we decompress `data1` using `gzip -d data1 -c > data2` and we do `file data2` we notice that is another compressed file but this time is compressed with `bzip2`. With this info now we know that not only this was heavily compressed but also compressed with different tools. With this info we can start writing a script in bash that will keep decommpressing this files until it finds something that is not compressed potentially the password to next level.

So we write the following script:

```bash
#!/bin/bash

# grabs first argument pass to our script
FILE=$1
WORKING_FILE='data'
COUNT=1

# decode hexdump back to binary file
xxd -r $1 > $WORKING_FILE$COUNT
# Control loop variable
FINISH=0

# continue looping until we find our password
while [ $FINISH -lt 1 ]
do
    # gets file type from file command of current working file
    file_type=`file $WORKING_FILE$COUNT`

    # check which tool was used to compressed the message by matching if substring exists in filetype
    case $file_type in
        *"gzip"*)
            gzip -d $WORKING_FILE$COUNT -c > $WORKING_FILE$((COUNT+1))
            echo "decompressing gzip"
            ;;
        *"bzip"*)
            bzcat $WORKING_FILE$COUNT > $WORKING_FILE$((COUNT+1))
            echo "decompressing bzip"
            ;;
        *"tar"*)
            tar -xOf $WORKING_FILE$COUNT > $WORKING_FILE$((COUNT+1))
            echo "decompressing tar"
            ;;
        *)
            cat $WORKING_FILE$COUNT
            let "FINISH++"
            ;;
    esac
    let "COUNT++"
done
```
we make the script executable as follow:
`chmod u+x decompresser.sh`

then we delete all the files in the tmp directory but the data.txt and we run the script as follow:

`./decompresser.sh data.txt`

Output:

```
decompressing gzip
decompressing bzip
decompressing gzip
decompressing tar
decompressing tar
decompressing bzip
decompressing tar
decompressing gzip
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```

> Note: If there was a different type of compressed file not listed in the script we could keep adding them and re run the script in order to keep it automated.

password: `8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL`