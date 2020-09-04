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

