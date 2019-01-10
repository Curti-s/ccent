- Chapter 1
******************
	Covers the following exam topics:
		* 1.0 Network Fundamentals
		* 1.1 Compare and Contrast OSi and TCP/IP models
		* 1.2 Compare and contrast TCP and UDP protocols
		
	Starts with a discussion of networking models, which give you the big picture view of the networking rules.
	
	Think of networking models as architectural plans for building a house. Networking model defines the rules abt how each part of the network should work as well as how parts should work together.
<<<<<<< HEAD
=======
	People building networking products and those that use them to build their own computer networks follow a particular networking model.

	CCNA exams include a detailed coverage of the TCP/IP networking model. The exams compare TCP/IP to OSi which was the first latrge effort to create a vendor-neutral networking model.
>>>>>>> 1657456a6e0893083b9d541a2268d1d150b660c9
	
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
		
<<<<<<< HEAD
		
- Overview of TCP/IP Networking Model
**************************************
	TCP/IP uses documents called Request For Comments (RFC). It has 2 alternative models:
		TCP/IP original:
=======

The network created by a corporation or an enterprise  for the purpose of allowing its employees to to communicate is known as **enterprise network**. 

Smaller networks used at home for business purposes are **small office/home office** SOHO networks.
		
- Overview of TCP/IP Networking Model
**************************************
	TCP/IP model defines and references a large collection of protocols that allow computers to communicate.

	TCP/IP uses documents called Request For Comments (RFC). It has 2 alternative models:
		
		TCP/IP original: RFC 1122
>>>>>>> 1657456a6e0893083b9d541a2268d1d150b660c9
			Application 
			Transport
			Internet
			Link
			
		TCP/IP Updated
			Application
			Transport
<<<<<<< HEAD
			Network
=======
			Network / Network Interface/ Network Access
>>>>>>> 1657456a6e0893083b9d541a2268d1d150b660c9
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
	It provides services to the application layer protocols that reside one layer
	higher in the TCP/IP model.
	
	NB - Each layer provides a service to the layer aboveit.
	
	- TCP Error Recovery Basics
	****************************
		TCP/IP requires a mechanism to guarantee delivery of data across a network. To recover from errors, TCP uses the concept of acknowledgements to recover from errors.
		
- IP Routing Basics
************************
	Uses (DDN) Dotted Decimal Notation. TCP/IP uses the IP protocol; providing a
	service for forwarding IP packets from one device to another.
	
 Data encapsulation refers to the process of putting header(and sometimes trailers) around data.
 
- Names of TCP/IP messages
------------------------------
	segment - > TCP & Data (Transport layer)
	packet - > IP & Data 	(Network layer)
	frame - > LH & Data & LT 	(Physical layer)
	
		(LH -> link header | LT -> link trailer)
		
- OSI layers and their functions
-----------------------------------
	Application layer -
		Provides an interface from the applications to the network by supplying a protocol with actions meaningful the the application, for instance, "get web page object".
		
	Presentation layer
		It negotiates data formats such as ASCII text or image types like JPEG and encryption.
		
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
<<<<<<< HEAD
		Define the physical xristics of the transmission medium, including connectors, pins, electrical currents,light modulation, encoing etc
=======
		Define the physical xristics of the transmission medium, including connectors, pins, electrical currents,light modulation, encoding etc
>>>>>>> 1657456a6e0893083b9d541a2268d1d150b660c9
		

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
<<<<<<< HEAD
=======

Steps for data encapsulation:

	1. Create and encapsulate the application data with any required application layer headers.
		For instance the HTTP OK message can be returned as a HTTP header.

	2. Encapsulate the data provided by the application layer inside the transport layer header.
		TCP or UDP header is typically used.

	3. Encapsulate the data provided by the transport layer inside the network layer (IP) header.

	4. Encapsulate the data provided by the network layer inside the data link ethernet header 
		and trailer.

	5. Transmit the bits.

### OSI layering concepts and benefits
Summary of benefits of layered protovol specifications:
	
	- Less complex: They break concepts into smaller parts.
	
	- Standard interfaces: Allow multiple vendors to create products that fill a
	particular role with all benefits of open competition.
	
	- Easier to learn
	
	- Easier to develop: Reducude complexity allows for easier program changes and
	faster product development
	
	- Multivedor interoperability: Comps and networking gear from multiple vendors can
	work in the same networ
	
	- Modular engineering: One vendor can write software that implements higher layers
	 for instance web browser - and another can write software that implements lower 
	 layers for example Microsoft built-in TCP/IP software in its OS
	 
 OSI uses a more generic term to refer to messages: Protocol Data Unit (PDU)
 
