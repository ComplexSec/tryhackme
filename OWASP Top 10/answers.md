#  TryHackMe - OWASP Top 10 (Room 008)

<details><summary>1 - Injection</summary>
<p>

Introduction: To complete the questions below, navigate to __http://MACHINE_IP/evilshell.php__

## Task 1.1

### Q: What strange test file is in the website root directory?

A: drpepper.txt

Walkthrough: A simple `ls` command gives us the name of a text file. Ideally, you would also check the root directory using `pwd`

![](/OWASP%20Top%2010/images/drpepper.png)

## Task 1.2

### Q: How many non-root/non-service/non-daemon users are there?

A: 0

Walkthrough: Using the `cut -d: -f1 /etc/passwd` gets only the usernames from /etc/passwd. Comparing this output with a similiar output on my own terminal tells us that there are no such non-special users

![](/OWASP%20Top%2010/images/no_users.png)

## Task 1.3

### Q: What user is this app running as?

A: www-data

Walkthrough: A simple `whoami` command reveals who the current user is

![](/OWASP%20Top%2010/images/wwwdata.png)

## Task 1.4

### Q: What is the user's shell set as?

A: /usr/bin/nologin

Walkthrough: To know about the current user's shell, fetch the contents of the /etc/passwd file. The 7th field contains login shells corresponding to the user. Looking at the www-data user, we can see the shell

![](/OWASP%20Top%2010/images/nologin.png)

## Task 1.5

### Q: What version of Ubuntu is running?

A: 18.04.4

Walkthrough: To determine the OS version we are running, use the `lsb_release -a` command

![](/OWASP%20Top%2010/images/version.png)

## Task 1.6

### Q: Print out the MOTD. What favourite beverage is shown?

A: Dr Pepper

Walkthrough: The `/etc/motd` is a file on Unix systems that contains a "message of the day", used to send a common message to all users. There are many MOTD files. The welcome message is located in the 00-header file

First, locate all .motd files and look for the 00-header file. Once found, simply cat out the contents

![](/OWASP%20Top%2010/images/header.png)

</p>
</details>

<details><summary>2 - Broken Authentication</summary>
<p>

## Task 2.1

### Q: What is the flag that you found in darren's account?

A: fe86079416a21a3c99937fea8874b667 

Walkthrough: We are given that there is an account named `darren` which contains a flag. To access this account, if we try something like " darren" or "   darren" for registering a new account and then try logging in with this account, we are able to access the account details

