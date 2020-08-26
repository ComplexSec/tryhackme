#  TryHackMe - Learn Linux (Room 001)

## Task 7 - `ls`

#### Q1: What flag outputs all entries?

A: -a

#### Q2: What flag outputs things in a long list format?

A: -l

## Task 8 - `cat`

#### Q1: What flag numbers all output lines?

A: -n

## Task 10 - Running a  Binary

#### Q: How would you run a binary called hello using the directory shortcut . ?

A: ./hello

#### Q: How would you run a binary called hello in your home directory using the shortcut ~ ?

A: ~/hello

#### Q: How would you run a binary called hello in the previous directory using the shortcut .. ?

A: ../hello

## Task 11 - `shiba1 binary`

#### Q: What is the password for shiba2

A: pinguftw

## Task 12 - `su`

#### Q: How do you specify which shell is used when you login?

A: `-s`

## Task 14 - `>`

#### Q: How would you output `twenty` to a file called test?

A: `echo twenty > test`

## Task 18 - `$`

#### Q: How would you set nootnoot equal to 1111?

A: `export nootnoot=1111`

#### Q: What is the value of the home environment variable?

a: `/home/shiba2`

## Task 21 - shiba2

#### Q: What is shiba3's password?

A: happynootnoises

## Task 24 - chmod

#### Q: What permissions mean the user can read the file, the group can read and write to the file, and no one else can read, write or execute the file?

A: 460

#### Q: What permissions mean the user can read, write and execute the file, the group can read, write, and execute the file, and everyone else can read, write, and execute the file?

A: 777

## Task 25 - chown

#### Q: How would you change the owner of file to paradox?

A: chown paradox file

#### Q: What about the owner and group of file to paradox?

A: chown paradox:paradox file

#### Q: What flag allows you to operate on every file in the directory at once?

A: -R

## Task 26 - rm

#### Q: What flag deletes every file in a directory?

A: -r 

#### Q: How do you suprress all warning prompts?

A: -f

## Task 27 - mv

#### Q: How would you move `file` to /tmp directory?

A: mv file /tmp

## Task 29 - cd && mkdir

#### Q: Using relative paths, how would you cd to your home directory?

A: cd ~

#### Q: Using absolute paths, how would you make a directory called test in /tmp?

A: mkdir /tmp/test

## Task 30 - ln

#### Q: How would you link /home/test/testfile to /tmp/test?

A: ln /home/test/testfile /tmp/test

## Task 31 - find

#### Q: How do you find files that have specific permissions?

A: -perm

#### Q: How would you find all the files in /home?

A: find /home

#### Q: How would you find all the files owned by paradox on the whole system?

A: find / -user paradox

## Task 32 - grep

#### Q: What flag lists line numbers for every string found?

A: -n

#### Q: How would you search for the string `boop` in the file `aaaa` in the directory `/tmp`?

A: grep boop /tmp/aaaa

## Task 33 - Shiba3

#### Q: What is shiba4's password?

A: test1234

## Task 34 - sudo

#### Q: How do you specify which user you want to run a command as?

A: -u

#### Q: How would you run whoami as user `jen`?

A: sudo -u jen whoami

#### Q: How do you list your current sudo privileges (what commands you can run, who you can run them as etc...)?

A: sudo -l

## Task 36 - adduser and addgroup

#### Q: How would you add the user `test` to the group `test`?

A: `sudo usermod -a -G test test`

## Bonus Challenge - The True Ending

#### Q: Finish this room off! What is the root.txt flag?

A: ad91979868d06e19d8e8a9c28be56e0c

#### Steps & Walkthrough

1. Check sudo privileges for each user

![](/Learn Linux/images/sudo_check.png)

2. Search for interesting files via `find` command

![](/images/interesting_file.png)

3. Check permissions of file

![](/images/perms.png)

4. Switch user to shiba2 and open file

![](/images/credentials.png)

5. Switch to nootnoot user and check privileges

![](/images/nootnoot.png)

6. Read the root.txt file located in /root/root.txt

![](/images/root.png)