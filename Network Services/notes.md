#  TryHackMe - Network Services (Room 015)

<details><summary>Understanding SMB</summary>
<p>

![](/Network%20Services/images/smb.png)

SMB (Server Message Block Protocol) is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network

Servers make file systems and other resources (printers, named pipes, APIs) available to clients on the network. Client computers may have their own hard disks, but they also want access to the shared file systems and printers on the servers

The SMB protocol is known as a __response-request protocol__ - meaning that it transmits multiple mesasges between the client and server to establish a connection. Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002), NetBEUI or IPX/SPX

Once a connection is established, clients can then send commands (SMBs) to the server that allow them to access shares, open files, read and write files, etc...

Microsoft Windows operating systems since Windows 95 have included client and server SMB protocol support. Samba, an open source server that supports the SMB protocol, was released for Unix systems

</p>
</details>

<details><summary>Enumerating SMB</summary>
<p>
	
![](/Network%20Services/images/smb2.png)

Enumeration is the process of gathering informaton on a target in order to find potential attack vectors and aid in exploitation

This process is essential for an attack to be successful, as wasting time with exploits that either do not work or can crash the system can be a waste of energy. Enumeration can be used to gather usernames, passwords, network information, hostnames, application data, services, or any other information

Typically, there are SMB share drives on a server that can be connected to and used to view or transfer files. SMB can often be a great starting point for an attacker looking to discover sensitive information

First step of enumeration is conducting a port scan to find out as much information as you can about the services, appications, structure and OS of the target machine. The `-A` flag for nmap enables __OS detection, Version detection, Script scanning and Traceroute__ all in one and the `-p-` flagf enables scanning across all ports (65,535)

Enum4Linux is a tool used to enumerate SMB shares on both Windows and Linux systems. It is basically a wrapper around the tols in the Samba package and makes it easy to quickly extract information from the target pertaining to SMB. Installed by default on Kali and Parrot but can install from the [official Github]https://github.com/portcullislabs/enum4linux)

The syntax for Enum4Linux is simple - `enum4linux [options] ip`

TAG | FUNCTION
------------ | -------------
-U | get userlist
-M | get machine list
-N | get namelist dump
-S | get sharelist
-P | get password policy information
-G | get group and member list
-A | all of the above (full basic enumeration)


</p>
</details>

<details><summary>Exploiting SMB</summary>
<p>
	
![](/Network%20Services/images/exploit.png)

While there are vulnerabilities such as [CVE-2017-7494](https://www.cvedetails.com/cve/CVE-2017-7494/) that can allow remote code execution by exploiting SMB, you are more likely to encounter a situation where the best way into a system is due to misconfigurations in the system

In this case, we are going to be exploiting anonymous SMB share access - a common misconfiguration that can allow us to gain information that will lead to a shell

From our enumeration, we know:

	* The SMB share location
	* The name of an interesting SMB share

SMBClient is part of the default Samba suite. While it is available by default on Kali and Parrot, you can find the documentation [here](https://www.samba.org/samba/docs/current/man-html/smbclient.1.html) if you need to install it

We can remotely access the SMB share using the syntax:

	`smbclient //[IP]/[SHARE]`

Followed by the tags:

	`-U [name]` to specify the user
	`-p [port]` to specify the port

</p>
</details>


<details><summary>Understanding Telnet</summary>
<p>
	
![](/Network%20Services/images/telnet.png)

Telnet is an application protocol which allows you to connect to and execute commands on a remote machine that is hosting a telnet server

The telnet client will establish a connection with the server. The client will then become a virtual terminal - allowing you to interact with the remote host

Telnet sends ALL messages in cleartext and has no specific security mechanisms. Thus, in many applications and services, Telnet has been replaced by SSH in most implementations

Telnet works when the user conects to the server using the Telnet protocol - entering __telnet__ into a command prompt. The user then executes commands on the server by using specific Telnet commands in the Telnet prompt. You can connect to a Telnet server with the following syntax:

	`telnet [ip] [port]`

</p>
</details>

<details><summary>Enumerating Telnet</summary>
<p>
	
![](/Network%20Services/images/enum.png)

We've already seen how key enumeration can be in exploiting a misconfigured network service. However, vulnerabilities that could be potentially trivial to exploit do not always jump out as us. For that reason we need to be thorough in our method

Always start out the same way by doing a port scan to find out as much informaton as we can about the services, applications, structure and OS of the target machine

Hop over to [answers](https://github.com/ComplexSec/tryhackme/blob/master/Network%20Services/answers.md) to continue

</p>
</details>

<details><summary>Exploiting Telnet</summary>
<p>
	
![](/Network%20Services/images/vuln.jpg)

Telnet, being a protocol, is insecure for being in cleartext. It lacks encryption so sends all communication over plaintext and for the most part has poor access control. There are CVE's for Telnet client and server systems so when exploiting you can check for those on

	https://www.cvedetails.com/
	https://cve.mitre.org/

A CVE - short for Common Vulnerabilities and Exposure - is a list of publicly disclosed computer security flaws. When someone refers to a CVE, they usually mean the CVE ID number assigned to a security flaw

You are far more likely to find a misconfiguration in how Telnet has been configured or is operating that will allow you to exploit it

From our enumeration stage, we know the following:

	* There is a poorly hidden telnet service running on this machine
	* The service itself is marked "backdoor"
	* We have a possible username of "Skidy" implicated

Using this information, we can try accessing the telnet port and using it as a foothold to get a full reverse shell on the machine

A "shell" can simply be described as a piece of code or program which can be used to gain code or command execution on a device. A reverse shell is a type of shell in which the target machine communicates back to the attacking machine

The attacking machine has a listening port on which it receives the connection resulting in code or command execution

![](/Network%20Services/images/reverse.png)

Hop over to [answers](https://github.com/ComplexSec/tryhackme/blob/master/Network%20Services/answers.md) to continue

</p>
</details>

<details><summary>Understanding FTP</summary>
<p>
	
![](/Network%20Services/images/ftp.png)

File Transfer Protocol (FTP) is a protocol used to allow remote transfer of files over a network. It uses a client-server model to do this and relays commands and data in a very efficient way

A typical FTP session operates using two channels

	A command (sometimes called the control) channel
	A data channel

As their names imply, the command channel is used for transmitting commands as well as replies to those commands, while the data channel is used for transferring data

FTP operates using a client-server protocol. The client initiates a connection with the server, the server validates whatever login credentials are provided and then opens the session

While the session is open, the client may execute FTP commands on the server

The FTP server may support either Active or Passive connections or both

	* In an active FTP connection, the client opens a port and listens. The server is required to actively connect to it
	* In a passive FTP connection, the server opens a port and listens (passively) and the client connects to it

Find more details on the technical function and implementation of FTP on the [Internet Engineering Task Force website](https://www.ietf.org/rfc/rfc959.txt). The IETF is one of a number of standards agencies who define and regulate internet standards

</p>
</details>

<details><summary>Enumerating FTP</summary>
<p>
	
![](/Network%20Services/images/ftp_enum.png)

We are going to be exploiting an anonymous FTP login to see what files we can access and if they contain any information that might allow us to pop a shell on the system. This a common pathway in CTF challenges, and mimics a real-life careless implementation of FTP servers

As we are logging into an FTP server, we are going to need to make sure there is an FTP client installed on the system. There should be one installed by default on most Linux operating systems - you can test if there is one by typine `ftp` into the console. If a prompt does not appear, simply install via the `sudo apt install ftp` command

Worth noting that some vulnerable versions of in.ftpd and some other FTP server variants return different responses to the `cwd` command for home directories which exist and those that don't. This can be exploited because you can issue cwd commands before authentication and if there is a home directory there is more than likely a user account to go with it

This vulnerability is documented [here](https://www.exploit-db.com/exploits/20745)

Hop over to [answers](https://github.com/ComplexSec/tryhackme/blob/master/Network%20Services/answers.md) to continue

</p>
</details>

<details><summary>Exploiting FTP</summary>
<p>
	
![](/Network%20Services/images/exploitation.jpg)

Similiarly to Telnet, when using FTP both the command and data channels are unencrypted. Any data sent over these channels can be intercepted and read

With data from FTP being sent in plaintext, if a man in the middle attack took place, an attacker could reveal anything sent through this protocol (such as passwords). An article written by [JSCape](https://www.jscape.com/blog/bid/91906/Countering-Packet-Sniffers-Using-Encrypted-FTP) demonstrates and explains this process using APR-Poisoning to trick a victim into sending sensitive information to an attacker rather than a legitimate source

When looking at an FTP server from the position we find ourselves in, an avenue we can exploit is weak or default password configurations

From our enumeration we know:
	
	* There is an FTP server running
	* We have a possible username

Using this information, we can try and brute force the password

Hydra is a very fast online password cracking tool which can perform rapid dictionary attacks against more than 50 protocols including Telnnet, RDP, SSH, FTP, HTTP, HTTPS, SMB, several databases and much more

If you need to download it, you can find it [here](https://github.com/vanhauser-thc/thc-hydra)

The syntax for the command we are going to use is:

	`hydra -t 4 -l [user] -P /usr/share/wordlists/rockyou.txt -vV 10.10.169.28 ftp`

TAG | FUNCTION
------------ | -------------
hydra | runs the hydra tool
-t 4 | number of parallel connections per target
-l [user] | points to the user who's account you are trying to compromise
-P [path to dictionary] | points to file containing the list of passwords
-vV | sets verbose mode to very verbose - shows each attempt
[IP] | IP of target machine
ftp / protocol | sets the protocol

</p>
</details>

<details><summary>Expanding Your Knowledge</summary>
<p>
	
![](/Network%20Services/images/further.png)

There will always be things that surpirse us all especially in the sometimes abstract logical problems of capture the flag challenges. But, as with anything, practice makes perfect. We can all look back on the things we have learnt after completing something challenging.

Here are some resources that might be useful to read after completing this room

* https://medium.com/@gregIT/exploiting-simple-network-services-in-ctfs-ec8735be5eef#
* https://attack.mitre.org/techniques/T1210/
* https://www.nextgov.com/cybersecurity/2019/10/nsa-warns-vulnerabilities-multiple-vpn-services/160456/

</p>
</details>