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

When the message is received by the second computer, it reverses the process - starting at the physical layer and workign up