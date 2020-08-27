#  TryHackMe - Common Linux Privesc (Room 004)

## Understanding Privesc

Privilege escalation involves going from a lower permission to a higher permission. It's the exploitation of a vulnerability, design flaw or configuration oversight in an operating system or app to gain unauthorized access to resources that are usually restricted from users

Priv esc lets you gain system administrator levels of access. Being admin allows you to:

* Reset passwords
* Bypass access controls to compromise protected data
* Edit software configurations
* Enable persistence, so you can access the machine again later
* Change privilege of users

## Direction of Privilege Escalation

![](/Common%20Linux%20Privesc/images/typesofprivesc.png)

There are two main privilege escalation variants:

### Horizontal Privilege Escalation

This is where you expand your reach over the compromised system by taking over a different user who is on the same privilege level as you. Allows you to inherit whatever files and access that user has. 

Can be used to gain access to another normal privileged user that happens to have an SUID file attached to their home directory which can be used to get super user access

### Vertical Privilege Escalation

This is where you attempt to gain higher privileges or access, with an existing compromised account. For local priv esc attacks, this might mean hijacking an account with admin privileges or root privileges

## Enumeration

__LinEnum__ is a simple bash script that performs common commands related to priv esc. Important to understand what commands LinEnum executes

### Getting LinEnum on Victim Machine

Two ways to get LinEnum on the victim machine:

First way is to start a Python web server using `python -m SimpleHTTPServer 8080` tfhen using `wget` on the victim to download it from the local machine

![](/Common%20Linux%20Privesc/images/linenum_hosted.png)
![](/Common%20Linux%20Privesc/images/linenum_download.png)

The other way is to copy the raw LinEnum code from the local machine and paste it into a new file on the target using __vim__ or __nano__, saving it with `.sh` extension and executing it

![](/Common%20Linux%20Privesc/images/linenum_writingfile.png)
![](/Common%20Linux%20Privesc/images/linenum_chmod.png)

## Understanding LinEnum Output

Output is broken down into different sections. The main sections are as follows:

* Kernel
* Can we read/write sensitive files
* SUID files
* Crontab contents

	### Kernel

	Kernel information is shown. Most likely a kernel exploit available for this machine

	### Can we read/write sensitive files

	World-writable files are shown. Files that any authenticated user can read/write to

	### SUID Files

	SUID is a special type of file permissions given to a file. Allows the file to run with permissions of whoever the owner is. If root, it runs with root permissions

	### Crontab contents

	Cron is used to schedule commands at a specific time. Scheduled commands/tasks are known as *cron jobs*. The `crontab` command creates a crontab file containing commands and instructions for the cron daemon to execute. 

## Abusing SUID/GUID Files

First step in Linux priv esc is checking for files with the SUID/GUID bit set - means that files can be run with permission of the file owner/group.

### SUID Binary

When special permission is given to each user, it becomes SUID or SGID. When extra bit "4" is set to user(Owner), it becomes SUID(set User ID) and when bit "2" is set to group, it becomes SGID (set Group ID)

The permissions to look for are

* SUID (__rws__-rwx-rwx)
* GUID (rwx-__rws__-rwx)

### Finding SUID Binaries

To locate SUID binaries, utilized the find command by using `find / -perm -u=s -type f 2>/dev/null` 

* `find` initiates the find command
* `/` searches the whole file system
* `-perm` searches for files with specific permissions
* `-u=s` any of the permission bits mode are set for the file. Symbolic modes are accepted
* `-type f` only searches for files
* `2>/dev/null` suppresses errors

## Exploiting Writable /etc/passwd

![](/Common%20Linux%20Privesc/images/grep_root.png)

From LinEnum, we spot that __user7__ is a member of the __root__ group with __gid 0__

Conclusion is that user7 can edit the __/etc/passwd/__ file

### What is /etc/passwd?

The __/etc/passwd/__ file stores user account information. Contains a list of the system's accounts and gives information like user ID, group ID, home directory, shell and more of each user

It should have general read permissions as many command utilities to map user IDs to usernames. Write access must ONLY be given to __root__

### Understanding /etc/passwd format

The fields are separated by a colon. Total of seven fields per entry. In order, the fields mean:

* Username

	Used when user logs in. Should be 1-32 characters

* Password
	
	An "x" character indicates the password is stored in __/etc/shadow__

* User ID (uid)

	Each user must be assigned an ID. __uid 0__ is reserved for root and __uid 1-99__ are reserved for other predefined accounts. Further UID (100-9999) are reserved by system for administrative and system accounts/groups

* Group ID (gid)
	
	The primary group ID stored in __/etc/group__ file

* User ID info

	Allows you to add extra information about the user like full name. This field used by the __finger__ command

* Home directory

	The absolute path to the directory the user will be in when they log in. If it does not exist, the users directory becomes __/__

* Command/shell

	The absolute path of a command or shell. Typically a shell, but does not have to be

### How to Exploit a Writable /etc/passwd

If you have a writable /etc/passwd file, simply write a new line entry according to the formula and create a new user. Add the password hash of our choice, and set the UID, GID and shell to root

## Escaping Vi Editor

Running `sudo -l` (or checking the LinEnum results) on the __user8__ account shows that they can run __vi__ with root privileges. This allows us to escape vim into a root shell. To escape Vi into a shell, use the `:!sh` command inside Vi

### Misconfigured Binaries and GTFOBins

If you find a misconfigured binary, a good place to look up how to exploit them is [GTFOBins](https://gtfobins.github.io/)

GTFOBins is a curated list of Unix binaries that can be exploited by an attacker to bypass local security restrictions

## Exploiting Crontab

The __cron daemon__ is a long running process that executes commands at specific dates and times. Can create a crontab file containing commands and instructions for the Cron daemon to execute

### Viewing Active Crontabs

Use the `cat /etc/crontab` command to view what cron jobs are scheduled

### Format of a Cronjob

Cronjobs exist in a certain format. The format is as follows:

* `#` = ID
* `m` = Minute
* `h` = Hour
* `dom` = Day of month
* `mon` = Month
* `dow` = Day of the week
* `user` = What user the command will run as
* `command` = What command should be run

### Exploiting

The autoscript.sh on user4's Desktop is scheduled to run every five minutes and is owned by root. We can create a command that will return a shell and paste it into the file.

