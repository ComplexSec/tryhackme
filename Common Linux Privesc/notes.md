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

The other way is to copy the raw LinEnum code from the local machine and paste it into a new file on the target using *vim* or *nano*, saving it with `.sh` extension and executing it

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