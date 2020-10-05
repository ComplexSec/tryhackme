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

	[CVE Details Website](https://www.cvedetails.com/)
	[CVE Mitre](https://cve.mitre.org/)


</p>
</details>
