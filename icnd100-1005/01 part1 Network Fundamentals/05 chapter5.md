-05 Fundamentals of TCP/IP Transport and Applications
*****************************************************
	Covers the following topics:
		1.0 Networking fundamentals
		1.2 Compare and contrast TCP and UPD protocols
		4.0 Infrastructure Services
		4.1 Describe DNS lookup operation
		
CCENT and CCNA Routing and Switching exams focus mostly on functions of the
lower layers of TCP/IP, that define how IP networks send IP packets from
host to host using LAN and WANs.
However this chapter explains the basics of a few topics which receive less
attention on the exam:
	TCP/IP transport layer &
	Application layer   which plays an important role in understanding the
basics before diving deeper into LANs and IP routing.

We begin examining the function of the 2 transport layer protocols:
	- Transmission Control Protocol (TCP) &
	- User Datagram Protocol (UDP)
The second major section will examine the TCP/IP Applicaion layer,
including how Domain Name System (DNS) works.



- Do I Know This Already?
**************************


1. Which of the following header fields identify which TCP/IP application
  gets data received by the computer?
  	
  	A. Ethernet Type
  	B. SNAP Protocol Type
  	C. IP Protocol
  	D. TCP Port Number
  	E. UDP Port Number
  	
  	>> TCP Port Number and UDP Port Number
  	
2.	Which of the following are typical functions of TCP?
	(Choose 4 answers)
	
	A. Flow control(windowing)
	B. Error Recovery
	C. Multipexing using port numbers
	D. Routing
	E. Encryption
	F. Ordered data transfer
		(A networking function,included in TCP, in which the protocol defines
		how the sending host should number the data segements transmitted,
		defines how the receiving device should attempt to reorder data if it 
		arrives out of order and specifies to discard the data if it cannot be
		delivered on order)
		
	>> Flow Control, Error Recovery, Multiplexing using port numbers and Order
	   transfer.
		
3.	Which of the following functions are performed by both TCP and UDP?
	
	A. Windowing
	B. Error revcovery
	C. Multiplexing using port numbers
	D. Routing
	E. Encryption
	F. Ordered data transfer
	
	>> Multipexing using port numbers 
	
4.	What do you call data that includes the layer 4 protocol header and data
	given to Layer 4 by the upper layers, not including any header and trailers
	from Layers 1 to 3? (Choose 2 answers)
		
	 A. L3PDU
	 B. Chunk
	 C. Segment
	 D. Packet
	 E. Frame
	 F. L4PDU
	 
	 >> Segment & L4PDU.
	 	
5.	In the URI http://www.certskills.com/ICND1, which part identifies the web
	web server?
		
	A. http
	B. www.certskills.com
	C. certskills.com
	D. http://www.certskills.com
	E. The file name.html includes the hostname
	
	>> www.certskills.com
	
6.	Fred opens a web browser and connects to the www.certskills.com website.
	Which of the following are typically true about what happens between Fred's
	web browser and the web server? (Choose 2 answers)
	
	A. Messages flowing toward the server use UDP destination port 80
	B. Messages flowing from the server typically use RTP
	C. Messages flowing to the client typically use a source TCP port number
	   of 80.
	D. Messages flowing to the server typically use TCP.
	
	>> Messages flowing to the client typically use a source TCP port number
	   80
	>> Messages flowing to the server typically use TCP
	
TCP/IP layer 4 protocols: TCP and UDP
**************************************

	OSI transport layer 4 defines several functions, most important of which are
	error recovery and flow control. Likewise TCP/IP transport layer protocols
	also implement the same type of features.
	
	Key difference between TCP and UDP is that TCP provides a wide range of features
	unlike UDP. For instance, routers discard packets for various reasons:
		- bit errors,
		- congestion,
		- instances in which no correct routes are known. etc
	TCP provides retransmission(error recovery) and helps to avoid congestion(flow
	control), unlike UDP. As a result many apps choose TCP.
	
	UDP requires fewer bytes in its header compare to TCP, hence fewer bytes of 
	overhead in the network. UDP software doesn't slow down data transfer in cases
	where TCP can purposefully slow down.
	Apps like (VoIP) Voice over IP & Video over IP do not need error recovery, therfore
	they use UDP.
	
	Table listing features of TCP/UDP, with only the first item supported by UDP
	
	Function  | Description
	********* | **************************************************************************
	
	Multiplexing using port numbers
		Function that allows receiving hosts to choose the correct application for
		which the data is destined, based on the port number.
		
	Error recovery (Reliability)
		Process of numbering and acknowledging data with Sequence and acknowledgement
		header fields.
		
	Flow Control using windowing
		Process that uses window sizes to protect the buffer space and routing devices
		from being overloaded with traffic.
		
	Connection establishment and termination
		Process used to initialize port numbers and sequence and acknowledgement fields.
		
	Ordered data transfer and data segmentation
		Continious stream of bytes from an upper-layer process that is "segemented"
		for transmission and delivery to upper layer processes at the receving device,
		with the bytes in the same order.
		
Transmission Control Protocol
*****************************
	Each TCP/IP application chooses whether to TCP or UDP bases on the application requirements.
	For instance TCP provides error recovery which uses more  processing cycles, unlike UDP which
	takes less bandwith and fewer processing cycles.
	
	TCP, as defined in RFC 793, accomplishes the functions listed in the table above,
	through mechanisms at the endpoint computers, regardless of whether 2 hosts are on 
	the same Ethernet or separated by the entire Internet.
	
	
	TCP header fields
	******************
	4 bytes
	Source Port                |              Destination port
	----------------------------------------------------------------
				    Sequence         Number
	----------------------------------------------------------------
				  Acknowledgement    Number
	-----------------------------------------------------------------
	Offset | Reserved   | Flag bits   |    Window
	-----------------------------------------------------------------
		    Checksum           |      Urgent
    ------------------------------------------------------------------
    
    
    The message created by TCP that begins with the TCP header, follwed by an 
    application data, is called a TCP segement. Alternatively, the more generic term
    is Layer 4 PDU or L4PDU.
    

Multiplexing using port numbers
********************************
	Both used in TCP and UDP.
	
	It involves the process of how a computer thinks when receiving data. It tells the
	receiving computer which application to give the received data.
	
	Multiplexing relies on a concept called a socket; consisting of 3 things;
		* IP address
		* Transfer protocol
		* Port number
		
			10.1.1.2,  TCP, port 80
			10.1.1.1,  TCP, port 1030
				Why 1030?
			Infact hosts typically allocate  dynamic port numbers starting at 1024
			because ports below 1024 are reserved for well known applications.
			
	Well known port numbers are used by servers; other port numbers are used by clients.
	
	Each client on the same host uses a different port number, but a server uses the
	same port number for all connections. For instance, 100 web browsers on the same
	host computer could each connect to a web server, but the web server with 100 clients
	connected to it would have only one socket & therefore, only one port number(port 80
	in this case).
	
	The webserver can tell which packets are sent from which client by looking at the
	source port of received TCP segments. The server can send data to the correct web
	client(browser) by sending data to that same port number.
	
	The same concept applies to UDP.
	NB::
		Find all RFCs at []!(www.rfc-editor.org/rfc/rfcxxx.txt), where xxx is the number of 
		the RFC.
		
Popular TCP/IP Applications
***************************/

	- WWW World Wide Web, exists through web browsers accesing the content available
	on web browsers. It can be used to manage routers or switches; when you enable
	web srever function in them.
	
	- Domain Naming System (DNS), uses a client/server model, with DNS servers being
	controlled by networking personnel and DNS client functions being part of most any
	device that uses TCP/IP today. The client simply asks the DNS server to suply the
	IP address that corresponds to a given name.
	
	- Simple Network Management Protocol (SNMP), is an application layer protocol
	used specifically for network device management. For instance, Cisco supplies
	a variety of network management software product family. They can be used to 
	query compile, store and display information about network's operation.
	
	- Traditionally, to move files from a router or switch, Cisco used Trivial File
	Transfer Protocol (TFTP), that defines a protocol for basic file transfer-hence 
	the word trivial. Alternatively, routers and switches can use File Transfer 
	Protocol (FTP) that allows more features, making it a general choice for the
	general end-user population.
	
	Some of these applications use either TCP or UDP. For instance, Simple Mail Transfer 
	Protocol (SNMP) and Post Office Protocol version 3 (POP3), both usedfor transferring
	mail, require guaranteed delivery; therefore they use TCP.
	
	Regardless of the transport layer protocol, applications use well-known port numbers
	so that clients know which port to attemp to connect to.
	
	eg
	Port number 20:
		Protocol: TCP
		Application: FTP data
		
	Port number 21:
		Protocol: TCP
		Application: FTP control
		
	Port number 22:
		Protocol: TCP
		Application: SSH
	
	Port number 23:
		Protocol: TCP
		Application: Telnet
		
	Port number 25:
		Protocol: TCP
		Application: SMTP
		
	Port number 53:
		Protocol: TCP / UDP
		Application: DNS
		
	Port number 67:
		Protocol: UDP
		Application: DHCP Server
		
	Port number 68:
		Protocol: UDP
		Application: DHCP Client
		
	Port number 69:
		Protocol: UDP
		Application: TFTP
		
	Port number 80:
		Protocol: TCP
		Application: HTTP(WWW)
		
	Port number 110:
		Protocol: TCP
		Application: POP3
		
	Port number 161:
		Protocol: UDP
		Application: SNMP
		
	Port number 443:
		Protocol: TCP
		Application: SSL
		
	Port number 514:
		Protocol: UDP
		Application: Syslog
		

Connection Establishment & Termination
****************************************
	TCP connection establishment occurs before any other TCP features.
	Connection establishment refers to the process of initializing 
	Sequence and Acknowledgement fields and agreeing on the port number used.
	
	Example
	
	Web browser                                             Web Server
	
	port 1027    --------SYN DPORT=80, SPORT=1027---------->  port 80
	             <------SYN ACK DPORT=1027, SPORT-80--------
	             -------ACK DPORT=80 SPORT=1027------------>
	             
	
	Three-way handshake TCP connection.
	
	SYN -> Synchronize the sequence
	ACK -> Acknowledge
	
	TCP connection termination. A four-way termination sequence. Uses an additional
	flag called FIN bit. Short for Finished.
	
	example
	
	
	PC1                                 PC2
	    --------ACK, FIN------------->
	    <-------ACK-------------------
	    <-------ACK FIN---------------
	    --------ACK------------------->
	    
	TCP (connection oriented) establishes and terminates connections between the
	endpoints, whereas UDP doesn't(Connectionless).
	
	Connection_oriented protocol:
		A protocol that requires exchange of messages before data transfer begins,
		or has a required established correlation between 2 endpoints
		
	Connectionless protcol:
		A protocol that neither requires an exchange of messages when data transfer
		begins, nor a pre-established correlation between 2 endpoints
    
### Error recovery and reliability

TCP provides for reliable data transfer which is alse called 
**reliability or error recovery**. It is accomplished through numbering data bytes using
sequence and acknowledgment fields in the TCP header.

The convention of acknowledging by listing the next expected byte, rather than the
number of the last byte received is called **forward acknowledgment**

### Flow control using windowing
TCP implements flow control using a window concept that is applied to the amount of
data that can be outstanding and waiting acknowledgment at any one point in time.
The window concept lets the receiving host tell the sender how much data it can
receive right now, giving the receiving host a way to make the sending host slow down
or speed up.
The receiver can slide the window size up or down - called **sliding window** or
**dynamic window.**

Examples might give one the impression that TCP makes hosts sit and wait for
acknowledgment alot.However, TCP does not want to make the sending host have to wait
to send data. For instance, if an acknowledgment is received before the window is 
exhausted, a new window begins and the sender continues sending data until the current
window is exhausted.

In a network with few problems, few lost segments and little congestion, the TCP window
stays relatively large with hosts seldom waiting to send,

### User datagram protocol
Provides a service for applications to exchange messages.
Connectionless.
Provides no reliability, no windowing, no reordering of received data and no 
segmentation of large chunks of data into the right size for transmission.
However it provides, data transfer and multipexing using port numbers, using fewer 
bytes of overhead and less processing required than TCP.

Only realtime communication and apps that are tolerant to data loss use UDP. For
instance, VoIP uses UDP because if a voice packet is lost, by the time the loss could be noticed and the packet retransmitted, too much delay would have occured and the voice would be unintelligible.
DNS requests use UDP because the user will retry an operation if the DNS resolution
fails.
The Network File System, a remote file system application, performs recovery with 
application layer code, therefore UDP features are acceptable.

UDP header format:
	has 8 bytes, compared to 20 bytes in TCP header
	
	|------------------- 4 bytes -------------------|
	   source port         |   destination port
	   length              |   checksum
	   

		 
