#  TryHackMe - Introductory Networking (Room 013)

<details><summary>Task 2 - OSI Model</summary>
<p>

## Task 2.1

### Q: Which layer would choose to send data over TCP or UDP?

A: 4 - Transport Layer

## Task 2.2

### Q: Which layer checks received packets to make sure that they have not been corrupted?

A: 2 - Data Link

## Task 2.3

### Q: In which layer would data be formatted in preparation for transmission?

A: 2 - Data Link

## Task 2.4

### Q: Which layer transmits and receives data?

A: 1 - Physical

## Task 2.5

### Q: Which layer encrypts, compresses, or otherwise transforms the initial data to give it a standardised format?

A: 6 - Presentation

## Task 2.6

### Q: Which layer tracks communications between the host and receiving computers

A: 5 - Session

## Task 2.7

### Q: Which layer accepts communication requests from applications?

A: 7 - Application

## Task 2.8

### Q: Which layer handles logical addressing?

A: 3 - Network

## Task 2.9 

### Q: When sending data over TCP, what would you call the "bite-sized" pieces of data?

A: Segments

## Task 2.10

### Q: Which layer would the FTP protocol communicate with?

A: 7 - Application

## Task 2.11

### Q: Which transport layer protocol would be best suited to transmit a live video?

A: UDP

</p>
</details>

<details><summary>Task 3 - Encapsulation</summary>
<p>
	
## Task 3.1

### Q: How would you refer to data at layer 2 of the encapsulation process (with the OSI model)?

A: Frames

## Task 3.2

### Q: How would you refer to data at layer 4 of the encapsulation process (with the OSI model), if the UDP protocol has been selected?

A: Datagrams

## Task 3.3

### What process would a computer perform on a received message?

A: De-encapsulation

## Task 3.4

### Q: Which is the only layer of the OSI model to add a __trailer__ during encapsulation?

A: Data Link

## Task 3.5

### Q: Does encapsulation provide an extra layer of security (Aye/Nay)?

A: Aye

</p>
</details>

<details><summary>Task 4 - TCP/IP Model</summary>
<p>
	
## Task 4.1

### Q: Which model was introduced first, OSI or TCP/IP?

A: TCP/IP

## Task 4.2

### Q: Which layer of the TCP/IP model covers the functionality of the Transport Layer of the OSI model (Full Name)?

A: Transport

## Task 4.3

### Q: Which layer of the TCP/IP model covers the functionality of the Session layer of the OSI model (Full Name)?

A: Application

## Task 4.4

### Q: The Network Interface layer of the TCP/IP model covers the functionality of two layers in the OSI model. These layers are Data Link and ...?

A: Physical

## Task 4.5
 
### Which layer of the TCP/IP model handles the functionality of the OSI network layer?

A: Internet

## Task 4.6

### Q: What kind of protocol is TCP?

A: Connection-based

## Task 4.7

### Q: What is SYN short for?

A: Synchronized

## Task 4.8

### Q: What is the second step of the three way handshake?

A: SYN/ACK

## Task 4.9

### Q: What is the short name for the Acknowledgement segment in the three-way handshake?

A: ACK

</p>
</details>

<details><summary>Task 5 - Wireshark</summary>
<p>
	
## Task 5.1

### Q: What is the protocol specified in the section of the request that is linked to the Application layer of the OSI and TCP/IP models?

A: Domain Name System

## Task 5.2

### Q: Which layer of the OSI model does the section that shows the IP address "172.16.16.77" link to (Name of the layer)?

A: Network

## Task 5.3

### In the section of the request that links to the Transport layer of the OSI and TCP/IP models, which protocol is specified?

A: User Datagram Protocol

## Task 5.4

### Over what medium has this request been made (linked to the Data Link layer of the OSI model)?

A: Ethernet II

## Task 5.5

### Which layer of the OSI model does the section that shows the number of bytes transferred (81) link to?

A: Physical

## Task 5.6

### [Research] Can you figure out what kind of address is shown in the layer linked to the Data Link layer of the OSI model?

A: MAC

</p>
</details>

<details><summary>Task 6 - [Networking Tools] Ping</summary>
<p>
	
## Task 6.1

### Q: What command would you use to ping the bbc.co.uk website?

A: ping bbc.co.uk

## Task 6.2

### Q: Ping muirlandoracle.co.uk. What is the IP address?

A: 217.160.0.152

## Task 6.3

### What switch lets you changed the interval of sent ping requests?

A: -i

## Task 6.4

### What switch would allow you to restrict requests to IPv4?

A: -4

## Task 6.5

### What switch would give you a more verbose output?

A: -v

</p>
</details>

<details><summary>Task 7 - [Networking Tools] Traceroute</summary>
<p>
	
## Task 7.2

### Q: What switch would you use to specify an interface when using Traceroute?

A: -i

## Task 7.3

### Q: What swithc would you use if you wanted to use TCP requests when tracing the route?

A: -T

## Task 7.4

### [Lateral Thinking] Which layer of the TCP/IP model will traceroute run on by default?

A: Internet

</p>
</details>

<details><summary>Task 8 - [Networking Tools] WHOIS</summary>
<p>
	
## Task 8.2 (facebook.com)

### What is the registrant postal code for facebook.com?

A: 94025

## Task 8.3 (facebook.com)

### When was the facebook.com domain first registered?

A: 29/03/1997

## Task 8.5 (microsoft.com)

### Which city is the registrant based in?

A: Redmond

## Task 8.6 (microsoft.com)

### [OSINT] What is the name of the golf course that is near the registrant address for microsoft.com?

A: Bellevue Golf Course

## Task 8.7 (microsoft.com)

### Q: What is the registered Tech Email for microsoft.com?

A: msnhst@microsoft.com


</p>
</details>
