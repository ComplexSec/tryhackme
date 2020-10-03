#  TryHackMe - Introductory Networking (Room 013)

<details><summary>The OSI Model: An Overview</summary>
<p>

![](/Introductory%20Networking/images/osi.png)

The OSI (Open Systems Interconnection) model is a standardized model which is used to demonstrate the theory behind networking

In practice, it is the more compact TCP/IP model that real-world networking is based off but the OSI model is easier to get an initial understanding from

The OSI model consists of seven layers:

* Application
* Presentation
* Session
* Transport
* Network
* Data Link
* Physical

## Layer 7 - Application

The application layer essentially provides networking options to programs running on a PC. It works almost exclusively with applications, providing an interface for them to use in order to transmit data. When data is given to the application layer, it is passed down into the presentation layer

## Layer 6 - Presentation

The presentation layer receives data from the application layer. This data tends to be in a format that the application understands but not necessarily in a standardized format that could be understood by the application layer in the __receiving computer__

The presentation layer translates the data into a standardized format, as well as handles __encryption, compression__ or other __transformations__ to the data. With this complete, the data is passed down to the session layer

## Layer 5 - Session

When the session layer receives the correctly formatted data from the presentation layer, it looks to see if it can set up a connection with the other computer across the network. If it cannot, it sends back an error and the process goes no further. If a session can be established, then it is the job of the session layer to maintain it, as well as co-operate with the session layer of the remote computer in order to synchronize communications

The session layer is particularly important as the session that it creates is unique to the communication in question. This is what allows you to make multiple requests to different endpoints simultaenously without all the data getting mixed up

When the session layer has successfully logged a connection between the host and remote comptuer, the data is passed down to the transport layer

## Layer 4 - Transport

The transport layer servers numerous important functions. Its first purpose is to choose the protocol over which the data is to be transmitted. The two most common protocols in the transport layer are TCP and UDP

With TCP, the transmission is connection-based which means that a connection between the computers is established and maintained for the duration of the request. This allows for a reliable transmission, as the connection can be used to ensure that the packets ALL get to the right place. A TCP connection allows the two computers to remain in constant communication to ensure that the data is sent at an acceptable speed, and that any lost data is re-sent

With UDP, the opposite is true. Packets of data are eseentially thrown at the receiving computer - if it cannot keep up then that's its problem

This means that TCP would usually be chosen for situations where accuracy is favoured over speed (file transfers, loading a webpage, etc...) and UDP would be used in situations where speed is more important (video streaming)

With a protocol selected, the transport layer then divides the transmission up into bite-sized pieces - over TCP they are called __segments__ and over UDP they are called __datagrams__ - which makes it easire to transmit the message successfully


## Layer 3 - Network

The network layer is responsible for locating the destination of your request. For example, the Internet is a huge network; when you want to request information from a webpage, it is the network layer that takes the IP address for the page and figures out the best route to take.

At this stage, we are working with what is referred to as __Logical Addressing__  which are still software controlled. Logical addresses are used to provide order to networks, categorizing them and allowing us to properly sort them

The most common form of logical addressing is the IPv4 format - 192.168.1.1 for example

## Layer 2 - Data Link

The data link layer focuses on the __physical addressing__ of the transmission. It receives a packet from the network layer and adds in the physical MAC address of the receiving endpoint. Inside every network enabled computer is a Network Interface Card (NIC) which comes with a unique MAC (Media Access Control) address to identify it

MAC addresses are set by the manufacturer and literally burnt into the card - they cannot be changed but can be __spoofed__. When information is sent across a network, it is the physical address that is used to identify where exactly to send the information

Additionally, it is the job of the data link layer to present the data in a format suitable for transmission

The data link layer also servers an important function when it receives data, as it checks the received information to make sure that it has not been corrupted during transmission, which would well happen when the data is transmitted by layer 1

## Layer 1

The physical layer is right down to the hardware. This is where the electrical pulses that make up data transfer over a network are sent and received. It is the job of the physical layer to convert the binary data of the transmission into signals and transmit them across the network, as well as receiving incoming signals and converting them back into binary data

</p>
</details>

<details><summary>Encapsulation</summary>
<p>

![](/Introductory%20Networking/images/internet.png)

As the data is passed down each layer of the model, more information containing details specific to the layer in question is added on to the start of the transmission

The header added by the Network layer would include things like the source and destination IP addresses, and the header added by the Transport layer would include (amongst other things) information specific to the protocol being used

The data link layer also adds a piece on at the end of the transmission, which is used to verify that the data has not been corrupted on transmission - also has the added bonus of increased security, as the data cannot be intercepted and tampered with without breaking the trailer

The whole process is referred to as __encapsulation__ - the process by which data can be sent from one computer to another

![](/Introductory%20Networking/images/encap.png)

Notice that the encapsulated data is given a different name at different steps of the process. In layers 7, 6 and 5, the data is simply referred to as __data__

In the transport layer, the encapsulated data is referred to as a __segment__ or a __datagram__ depending on whether TCP or UDP has been selected.

At the network layer, the data is referred to as __packets__. When the packets get passed down to the Data Link layer, it becomes a __frame__ and by the time it is transmitted across a network, the frame is broken down into __bits__

When the message is received by the second computer, it reverses the process - starting at the physical layer and working up until it reaches the application layer, by stripping off the added information as it goes - referred to as __de-encapsulation__

Computers all follow the same process of encapsulation to send data and de-encapsulation upon receiving it

The process of encapsulation and de-encapsulation are very important - they give us a standardised method for sending data. All transmissions will consistently follow the same methodology, allowing any network enabled device to send a request to any other reachable device

</p>
</details>

<details><summary>TCP/IP Model</summary>
<p>
	
![](/Introductory%20Networking/images/tcpip.png)

The TCP/IP model serves as the basis for real-world networking. It consists of only four layers - Application, Transport, Internet and Network Interface

The two models layers match up something like this

![](/Introductory%20Networking/images/match.png)

Process of encapsulation and de-encapsulation work in exactly the same way with TCP/IP model

TCP/IP takes it names from the two most important suite of protocols - __Transmission Control Protocol__ that controls the flow of data between two endpoints and the __Internet Protocol__ which controls how packets are addresses and sent

TCP is a __connection based__ protocol. Before sending any data via TCP, you must first form a stable connection between two computers. Process off orming this connection is called the __three-way handshake__

When you attempt to make a connection, your computer first sends a special request to the remote server indicating that it wants to initialize a connection. This request contains something called a __SYN__ bit which makes first contact in starting the connection process

The server responds with a packet containing the SYN bit as well as another acknowledgement bit called __ACK__

Finally, your computer will send a packet that contains the ACK bit by itself, confirming that the connection has been setup successfully

With the 3-way handshake completed, data can be reliably transmitted between the two computers. Any data that is lost or corrupted on tranmissions is re-sent, leading to a connection which appears to be lossless

To begin with there was no standardisation - different manufacturers followed their own methodologies, and consequently systems made by different manufacturers were completely incompatible when it came to networking

The TCP/IP model was introduced by the American DoD in 1982 to provide a standard

Later, the OSI model was also introduced by the International Organization for Standardisation (ISO); however, it is mainly used as a more comprehensive guide for learning
</p>
</details>

<details><summary>WireShark</summary>
<p>
	
![](/Introductory%20Networking/images/wireshark.png)

Wireshark is a tool used to capture and analyzed packets of data going across a network

When you first load the packet into WireShark, you are given a list of captured data in the top window. In the bottom two windows, you are shown the data contained in each captured packet of data

![](/Introductory%20Networking/images/pcap1.png)

Looking at the first packet, there are 5 pieces of information:

* Frame 1 - this shows details from the __physical__ layer of the OSI model (Network Interface layer of the TCP/IP model): the size of the packet received in terms of bytes
* Ethernet II - shows the details from the __Data Link__ layer of the OSI model (Network interface layer of the TCP/IP model): the transmission medium (in this case Ethernet), as well as the source and destination MAC addresses of the request
* Internet Protocol Version 4 - shows details from the __Network Layer__ of the OSI model (Internet Layer of the TCP/IP model): the source and destination IP addresses of the requests
* Transmission Control Protocol - shows details from the __Transport Layer__ of the OSI and TCP/IP models: in this case, it tells us that the protocol was TCP along with other things
* HyperText Transfer Protocol - shows details from the __Application Layer__ of the OSI and TCP/IP models: specifically, this is a HTTP GET request which requests a web page from a remote server

![](/Introductory%20Networking/images/wireshark2.png)

</p>
</details>

<details><summary>[Networking Tools] Ping</summary>
<p>
	
![](/Introductory%20Networking/images/ping.png)

The ping command is used when we want to test whether a connection to a remote resource is possible

Ping works by using the ICMP protocol, which is one of the slightly less well-known TCP/IP protocols. The ICMP protocol works on the __Network__ layer of the OSI model, and thus the Internet layer of the TCP/IP model. Ping can also be used to determine the IP address of the server hosting a website (eg. google.com)

One of the big advantages of ping is that it is ubiquitous to any network enabled device. All operating systems support it out of the box and even most embedded devices can use ping

</p>
</details>

<details><summary>[Networking Tools] Traceroute</summary>
<p>
	
![](/Introductory%20Networking/images/trace.png)

The internet is made up of many different servers and end-points, all networked up to each other. This means that in order to get to the content you actually want you first need to go through a bunch of other servers. Traceroute allows you to see each of these connections - it allows you to see every intermediate step between your computer and the resource you requested

By default, traceroute operates using the same ICMP protocol that ping utilizes - this can be altered with switches

![](/Introductory%20Networking/images/traceroute.png)

</p>
</details>

<details><summary>[Networking Tools] WHOIS</summary>
<p>
	
![](/Introductory%20Networking/images/dns.png)

Domains are leased out by companies called Domain Registrars. If you want a domain, you go and register with a registar, then lease the domain for a certain length of time

WHOIS allows you to query who a domain name is registered to. In Europe, personal details are redacted; however, elsewhere you can potentially get a great deal of information

There is a [web version](https://www.whois.com/whois/) available

![](/Introductory%20Networking/images/whois.png)

Some information you can gather from WHOIS can be:

* The domain name
* The company that registered the domain
* The last renewal & when it's next due
* Information about nameservers

</p>
</details>