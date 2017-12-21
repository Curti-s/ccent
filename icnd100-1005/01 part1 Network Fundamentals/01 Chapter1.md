- Chapter 1
******************
	Covers the following exam topics:
		* 1.0 Network Fundamentals
		* 1.1 Compare and Contrast OSi and TCP/IP models
		* 1.2 Compare and contrast TCP and UDP protocols
		
	Starts with a discussion of networking models, whic give you the big picture view of the networking rules.
	
	Think of networking models as architectural plans for building a house. Networking model defines the rules abt how each part of the network should work as well as how parts should work together.
	
- Do I Know This Already?
*************************
	1. Examples of TCP/IP transport layer protocols?
		TCP and UDP
		
	2. Examples of TCP/IP data-link layer protocols?
		Ethernet and PPP
		
	3.  The process of HTTP asking TCP to send some data and making sure that it is received correctly is an example of?
		Adjacent-layer interaction
		
	4. The process of TCP on one comp marking a TCP segement as 1 and the receiving comp then acknowledging the receipt of TCP segement1 is an example of?
		Transport-layer data segmentation and acknowledgement of sent packets.
		
	5.  The proces of a web server adding a TCP header to the contents of a web page, followed by adding an IP header and then adding a data link header and trailer is an example of?
		Data encapsulation
		
		
- Overview of TCP/IP Networking Model
**************************************
	TCP/IP uses documents called Request For Comments (RFC). It has 2 alternative models:
		TCP/IP original:
			Application 
			Transport
			Internet
			Link
			
		TCP/IP Updated
			Application
			Transport
			Network
			Data Link
			Physical
			
	TCP/IP original model is listed in RFC 1122,that breaks it into 4 layers. It has also been referred to as network access and network interface layer.
	
	Example of protocols:
		TCP/IP (original)
		Application   -> HTTP, POP3,SMTP
		Transport   -> TCP, UDP
		Internet   -> IP
		Link   -> Ethernet, Point-to-Point Protocol, T1
		
- TCP/IP Application layer
-----------------------------------
	Application layer provides an interface between the software running in the computer and the network.
	Generally the HTTP protocol is used. Was first created by Tim Berners Lee in the early 1990s. He gave HTTP the functionality to ask for contents of the web pages, specifically by giving the web browser the ability to request files from the server  and providing a wayfor the server to return the content of those files.
	Generally protocols use headers as a place to put information used by that protocol. HTTP headers include the request to "get" a file.


- TCP/IP Transport layer
**************************
	Most commonly used protocols:
		- TCP
		- UDP
	It provides services to the application layer protocols.
	
	- TCP Error Recovery Basics
	****************************
		TCP/IP requires a mechanism to guarantee delivery of data across a network. To recover from errors, TCP uses the concept of acknowledgements to recover from errors.
		
- IP Routing Basics
************************
	Uses (DDN) Dotted Decimal Notation. TCP/IP uses he IP protocol; providing a service for forwarding IP packets from one device to another.
	
 Data encapsulation refers to the process of putting header(and sometimes trailers) around data.
 
- Names of TCP/IP messages
------------------------------
	segment - > TCP & Data (Transport layer)
	packet - > IP & Data 	(Network layer)
	frame - > LH & Data & LT 	(Physical layer)
	
		(LH -> link header | LT _> link trailer)
		
- OSI layers and their functions
-----------------------------------
	Application layer -
		Provides an interface from the applications to the network by supplying a protocol with actions meaningful the the application, for instance, "get web page object".
		
	Presentation layer
		It negotiates data formats such as ASCII text or image types like JPEG
		
	Session layer
		Provides methods to group multiple bidirectional messages into a workflow for easier management and easier backout of work that happened if the entire network fails.
		
	Transport layer
		Focuses on data delivery between the 2 endpoints of a host.
		Also provides port addressing capabilities.
		
	Network layer
		Defines the logical addressing,routing(forwarding) and the routing protocols used to learn routes.
		
	Data-link layer
		Defines the protocols for delivering data over a particular single type of physical network. eg Ethernet data link protocols.
		
	Physical layer
		Define the physical xristics of the transmission medium, including connectors, pins, electrical currents,light modulation, encoing etc
		

- Benefits of layered protocols
	* Less complex by breaking networking models concepts into smaller parts
	* Standard interface definitions between each layer to allow for vendors to create products which fill that particular role with all benefits of open competition.
	* Easier to learn.
	* Easier to develop
	* Multivendor interoperability whereby vendors meet the same networking standards for their networking gear.
	* Modular engineering whereby one vendor can write software that implements higher layers eg. web browser, and another vendor can write software that implements lower layers eg Microsoft built-in TCP/IP software in OS
	
- OSI Encapsulation terminology
********************************
	In order to provide services to the next lower layer, each layer needs to make use of a header and possibly a trailer.
	OSI uses a more generic term to refer to messages, rather than a frame, packet and segment; PDU --> Protocol Data Unit which presents the bits and includes the headers and trailers for that layer as well as encapsulated data.
