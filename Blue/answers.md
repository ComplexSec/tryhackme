#  TryHackMe - Blue (Room 017)

## Please try and answer all questions before looking at the answers to test your knowledge :)

![](/Blue/images/msf4.png)

<details><summary>Task 1 - Recon</summary>
<p>
	
## Task 1.1

### Scan the machine

A: Use nmap with your favourite arguments and parameters. For me personally, I like using `nmap -A -T4 -p- <IP> -oA nmap`

![](/Blue/images/nmap.png)

## Task 1.2

### How many ports are open with a port number under 1000?

A: Looking at our nmap scan results, we can see that there are 3 ports under 1000 that are classified as open

![](/Blue/images/3ports.png)

## Task 1.3

### What is this machine vulnerable to?

A: Given the phrasing of the queston, we can assume this machine is vulnerable to a specific exploit. There are scripts available in nmap that scan for certain vulnerabilities - we can invoke and use them via the `--script vuln` parameter on nmap

![](/Blue/images/scrip.png)

</p>
</details>

<details><summary>Task 2 - Gain Access</summary>
<p>
	
## Task 2.1

### Start Metasploit

A: Simply done by typing `msfconsole` into the CLI

![](/Blue/images/msf.png)

## Task 2.2

### Find the exploitation code we will run against the machine and find the full path of the code

A: Using the `search` function inside msfconsole, we can search for either ms17-010 or eternalblue and it will show a list of results

![](/Blue/images/ms17.png)

## Task 2.3

### Show options and set the one required value - what is the name of this value?

A: In the options sub-section, there is a parameter called RHOSTS (Remote Hosts) which is our target IP. In the required field, we can see it is required

![](/Blue/images/rhosts.png)

## Task 2.4

### Run the exploit

A: Simply run the exploit via the `run` or `exploit` command

![](/Blue/images/run.png)

## Task 2.5

### Confirm the exploit ran correctly and background the shell via CTRL+Z

</p>
</details>

<details><summary>Task 3 - Escalate</summary>
<p>
	
## Task 3.1

### Research online how to convert a shell to a meterpreter shell in Metasploit and find the name of the post module 

A: Doing a bit of [googling](https://www.hackingarticles.in/command-shell-to-meterpreter/), we find a module called post/multi/manage/shell_to_meterpreter

![](/Blue/images/meter.png)

## Task 3.2

### Select this and show the options - what option are we required to change?

A: Looking through the options and the required field, we see there is a filed that says yes - this field is SESSION

![](/Blue/images/session.png)

## Task 3.3

### Set the required option

A: If we type `sessions` into msfconsole, we will see our current sessions. Our current session is labelled as session 1 so we set the SESSION to 1

![](/Blue/images/1.png)

## Task 3.4

### Run the module - if it does not work, try completing the previous exploit again

![](/Blue/images/complete.png)

## Task 3.5

### Once the meterpreter shell conversion completes, select that session for use

A: To select the session we just created, simply type `sessions 2` with 2 being the number of our meterpreter session

![](/Blue/images/2.png)

## Task 3.6

### Verify we have escalated to NT AUTHORITY\SYSTEM - run `getsystem` to confirm this

A: Typing `getsystem` in our meterpreter shell indicates we got system and typing `getuid` confirms we are the SYSTEM user

![](/Blue/images/system.png)

## Task 3.7

### List all processes running via `ps` command and find a process towards the bottom of the list running as SYSTEM and note the process ID

![](/Blue/images/ps.png)

A: You can follow this guidance yourself and pick one. Personally, I like to pick the service called `winlogon.exe` as it is consistently stable and is almost always present on a Windows system

To migrate to a process name rather than ID, use the `-N` parameter instead

![](/Blue/images/winlog.png)

</p>
</details>

<details><summary>Task 4 - Cracking</summary>
<p>
	
## Task 4.1

### Within our elevate meterpreter shell, run the `hashdump` command and find the non-default username - this dumps all passwords on the machine as long as we have the privileges

A: Running the command, we see all the password hashes. The non-default username is Jon

![](/Blue/images/jon.png)

## Task 4.2

### Copy the password hash to a file and research how to crack it - what is the password?

A: First of all, I extracted the hash into a file on my Windows 10 machine since I have a powerful GPU. Then, I ran the following command on hashcat - `hashcat64.exe -m 1000 -a 0 hashes.txt rockyou.txt` where hashes.txt is my extracted hashes and rockyou.txt is the wordlist

Once it is cracked, you can check the hashcat.potfile to see the cracked password

![](/Blue/images/cracked.png)

</p>
</details>

<details><summary>Task 5 - Find Flags!</summary>
<p>
	
## Flag 1

A: Flag1 is simply located in the base C: drive folder - simply navigate to it and use the `type` command to print the contents of it

![](/Blue/images/flag1.png)

## Flag 2

A: Flag2 hint tells us that Windows does not really like the location of the flag and can occassionally delete it and that it may be necessary to terminate/restart the machine and rerun the exploit to find it. 

The hint tells us that "I wish I wrote down where I kept my password. Luckily it's still stored here on Windows" - this hints at the SAM file configuration which is similiar to passwd on Linux

![](/Blue/images/flag2.png)

## Flag 3

A: Flag3 hint tells us that we need to have elevated privileges to access the flag. This hints at the file being somewhere only an administrator can access. One of the most valuable places to look is the desktop

Earlier, we located a user called Jon - let's see if we can access his desktop and see what files are there

![](/Blue/images/desk.png)

Hmmm.. it's not there. Another valuable place is in the Documents folder instead

![](/Blue/images/flag4.png)

Perfect. Always check common folders where people would store valuable documents like Documents, Desktop, etc....

</p>
</details>