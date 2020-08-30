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

Walkthrough: We are given that there is an account named `darren` which contains a flag. To access this account, if we try something like " darren" or "   darren" for registering a new account it successfully lets us create an account

![](/OWASP%20Top%2010/images/darren.png)

Once registered, simply log in as our darren (with spaces) and we will see the flag

![](/OWASP%20Top%2010/images/loggedin.png)

## Task 2.2

### Q: Now try to do the same trick and see if you can login as arthur

Walkthrough: Simply do the same as above but use arthur instead of darren

## Task 2.3

### Q: What is the flag you found in arthur's account?

A: d9ac0f7db4fda460ac3edeb75d75e16e

Walkthrough: Simply do the same method as Darren's account and we are able to receive the flag

As a note, trying various other methods like `arthur.`, `art hur`, `_arthur` yield no results. Only blank spaces can be used to check Broken Authentication successfully

![](/OWASP%20Top%2010/images/arthur.png)

</p>
</details>

<details><summary>3 - Sensitive Data Exposuer</summary>
<p>

## Task 3.1

### Q: Have a look around the webapp. The developer has left themselves a note indicating that there is sensitive data in a specific directory. What is the name of the mentioned directory?

A: /assets

Walkthrough: Looking at the source code on the /login page reveals the comment

![](/OWASP%20Top%2010/images/assets.png)

## Task 3.2

### Q:  Navigate to the directory you found in questionn one. What file stands out as being likely to contain sensitive data?

A: webapp.db

Walkthrough: There is a .db file which indicates a database. Databases normally store sensitive information in web apps

![](/OWASP%20Top%2010/images/webapp.png)

## Task 3.3

### Q: Use the supporting material to access the sensitive data. What is the password hash of the admin user?

A: 6eea9b7ef19179a06954edd0f6c05ceb

Walkthrough: First, download the webapp.db file. After downloading it, access it using the SQL commands located in [notes.md](https://github.com/ComplexSec/tryhackme/blob/master/OWASP%20Top%2010/notes.md) to access the database and get information

Revealing what the data means, we know that the third field indicates the password hash

![](/OWASP%20Top%2010/images/adminhash.png)

## Task 3.4

### Q: Crack the hash. What is the admin's plaintext password?

A: qwertyuiop

Walkthrough: Simply paste the hash into [Crackstation](https://crackstation.net/) and it will return the plaintext password

![](/OWASP%20Top%2010/images/adminhash.png)

## Task 3.5

### Q: Login as the admin. What is the flag?

A: THM{Yzc2YjdkMjE5N2VjMzNhOTE3NjdiMjdl}

Walkthrough: Simply login with the credentials found and get the flag

![](/OWASP%20Top%2010/images/flag.png)

</p>
</details>

