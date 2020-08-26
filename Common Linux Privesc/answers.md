#  TryHackMe - Common Linux Privesc (Room 004)

## Important Information

To start this test, login using the credentials __user3:password__

## Task 4.1

#### Q: What is the target's hostname?

A: polobox

Walkthrough: Learnt through __LinEnum.sh__ or by running the `hostname` command

![](/Common%20Linux%20Privesc/images/hostname_through_linenum.png)
![](/Common%20Linux%20Privesc/images/hostname_through_command.png)

## Task 4.2

#### Q: Look at the output of /etc/password. How many "user[x]" are there on the system?

A: 8

Walkthrough: Learnt through __LinEnum.sh__ or by running the `cat /etc/passwd` command

![](/Common%20Linux%20Privesc/images/passwd_through_linenum.png)
![](/Common%20Linux%20Privesc/images/passwd_through_command.png)

## Task 4.3

#### Q: How many available shells are there on the system?

A: 4

Walkthrough: Learnt through __LinEnum.sh__ or by running the `cat /etc/shells` command

![](/Common%20Linux%20Privesc/images/shells_through_linenum.png)
![](/Common%20Linux%20Privesc/images/shells_through_command.png)

## Task 4.4

#### Q: What is the name of the bash script that is set to run every 5 minutes by cron?

A: autoscript.sh

Walkthrough: Learnt through __LinEnum.sh__ or by running the `cat /etc/crontab` command

![](/Common%20Linux%20Privesc/images/crontab_through_linenum.png)
![](/Common%20Linux%20Privesc/images/crontab_through_command.png)

## Task 4.5

#### What critical file has had its permissions changed to allow some users to write to it?

A: /etc/passwd

Walkthrough: Learnt through __LinEnum.sh__ or by running the `ls -l /etc/passwd` command

![](/Common%20Linux%20Privesc/images/sens_through_linenum.png)
![](/Common%20Linux%20Privesc/images/sens_through_command.png)

## Task 5.1

### What is the path of the file in user3's directory that stands out to you?

A: /home/user3/shell

Walkthrough: Learnt through the [`find`](https://github.com/ComplexSec/tryhackme/blob/master/Common%20Linux%20Privesc/notes.md) command located in notes.md

![](/Common%20Linux%20Privesc/images/find_suid.png)

## Task 5.2 - no answer needed

We know that "shell" is a SUID bit file, therefore running it will run the script as a root user. Run it

## Task 5.3 - no answer needed

You should have a root shell

![](/Common%20Linux%20Privesc/images/root_shell.png)