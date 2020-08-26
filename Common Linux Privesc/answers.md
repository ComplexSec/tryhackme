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

## Task 6.1 - no answer needed

First, exit out of root by typing `exit` and swap to user using the `su -l user7` command. The password is __password__

## Task 6.2

### Q: What direction privilege escalation is this attack?

A: Vertical

Walkthrough: Learnt through the diagram at the very top

## Task 6.3

### Q: Before we add our new user, we first need to create a compliant password hash to add. We do this by using the command: "openssl passwd -1 -salt [salt] [password]"

### What is the hash created by using this command with the salt "new" and the password "123"?

A: $1$new$p7ptkEKU1HnaHpRtzNizS1

Walkthrough: Learnt through executing the command

![](/Common%20Linux%20Privesc/images/openssl.png)

## Task 6.4

### Now, we need to take this value and create a new root account. What would the /etc/passwd entry look like for a root user with the username "new" and the password hash we created?

A: new:$1$new$p7ptkEKU1HnaHpRtzNizS1:0:0:root:/root:/bin/bash

Walkthrough: Learnt through the [/etc/passwd format](https://github.com/ComplexSec/tryhackme/blob/master/Common%20Linux%20Privesc/notes.md) section inside in notes.md

## Task 6.6

### Q: Now, use "su" to login as the "new" account. You should be greeted with a root prompt

![](/Common%20Linux%20Privesc/images/root_shell2.png)

## Task 7.1 - no answer needed

### Q: First, swap user to user8 with the password of `password` using the `su -l user8` command

## Task 7.2

### Q: Using the `sudo -l` command, what does user8 require (or not require) to run vi as root?

A: NOPASSWD

Walkthrough: Learnt through running the `sudo -l` command

## Task 7.3 - no answer needed

### Q: All we need to do is open vi as root by typing `sudo vi`

## Task 7.4 - no answer needed

### Q: Now, type `:!sh` to open a shell from Vi

![](/Common%20Linux%20Privesc/images/vi_shell.png)
