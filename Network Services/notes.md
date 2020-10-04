#  TryHackMe - Network Services (Room 015)

<details><summary>Understanding SMB</summary>
<p>

![](/Network%20Services/images/smb.png)

SMB (Server Message Block Protocol) is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network

Servers make file systems and other resources (printers, named pipes, APIs) available to clients on the network. Client computers may have their own hard disks, but they also want access to the shared file systems and printers on the servers

The SMB protocol is known as a __response-request protocol__ - meaning that it transmits multiple mesasges between the client and server to establish a connection. Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002), NetBEUI or IPX/SPX

Once a connection is established, clients can then send commands (SMBs) to the server that allow them to access shares, open files, read and write files, etc...

Microsoft Windows operating systems since Windows 95 have included client and server SMB protocol support. Samba, an open source server that supports the SMB protocol, was released for Unix systems