- Chapter 4
********************
- Fundamentals of IPv4 Addressing and Routing
**************************************************
	Covers the following  exam topics
	3.0 Routing and Switching
	3.1 Describe the routing concepts
	3.1a Packet handling along the path through a network
	3.1b Forwarding decision based on route lookup
	3.1c Frame rewrite
	

TCP/IP network layer 3 defines how to deliver IP packets over the entire trip, from the original device that creates the packet to the device that needs to receive the packet.
	Cooperating functions required to route packets:
		* IP routing:
			The process of hosts and routers forwarding IP packets(Layer 3 PDU), 
			while relying on the underlying LAN and WAN
		* IP addressing:
			The address which is used to identify a packets's source and destination 
			host computer. Addressing rules organize addresses into groups,
			which greatly assist the routing process.
		* IP routing protocol:
			Protocol that aids routers by dynamically learning about the IP address
			groups, so that a router knows where to route the IP packets to the right
			destination.
		* Other utilities:
			Which include Domain Naming System, Address Resolution Protocol and Ping.
			
NB::
	This functions have variations for both well established IPv4 and IPv6. However, we focus on IPv4 in this chapter.
	
- Do I Know This Already?
***************************
	1.Which of the following are functions of the OSI layer 3 protocol?
		Logical addressing
		Path selection
		
	2.Which of the following is a valid Class C IP address that an be
	  assigned to a host?
	  	200.1.1.1
	  	from 192 to 223
	  	
	3.What is the assignable range of values for the first octet for class A IP networks?
		1 to 126
		
	4.PC1 and PC2 are on 2 different Ethernet LANs that are separated by an IP router.PC1's IP address is 10.1.1.1 and no subnetting is used. Which of the following addresses could be used for PC2?
		In consideration to classA network and the fact that no subnetting
		has occurred, the Ethernet LAN connected at PC2 will be on a different network, therefore
		9.1.1.1
		1.1.1.1
		
	5.Imagine a network with 2 routers that are connected with a point-to-point HDLC serial link. Each router has an Ethernet, with PC1 sharing the Ethernet with Router1 and PC2 sharing the Ethernet with Router2. When PC1 sends data to PC2, which of the following is true?
		Router1 strips the Ethernet header and trailer off the frame received from PC1, never to be used again.
		HDLC protocol will exist between 2 point-to-point routers inorder to link two LAN connections into a WAN (hence simulating a crossover cable).
	
	6.Which of the following does a router normally use when making a decision about routing TCP/IP packets?
		Destination IP address.
		
	7.Which of the following is true about LAN-connected TCP/IP host and its IP routing(forwarding) choices?
		The host sends packets to its default gateway if the destination IP address is in a different class of IP network than the host.
		The host sends packets to its default gateway if the destination IP address is in a different subnet than the host.
		
	8.Which of the following are function of a routing protocol?
	?????
		Learning routes for subnets directly connected to the router
		Forwarding IP packets based on a packet's destination IP address.
		
	9.A company implements a TCP/IP network, with PC1 sitting in an Ethernet LAN. Which of the following protocols and features requires PC1 to learn information from some other server device?
		DNS Domain Naming System
		
		1 A and C 2 B 3 D 4 D and F 5 A 6 C 7 B and C 8 A and 9 C
		
		
- Network layer routing logic (Forwarding)
********************************************
	PC1--------->Router1------->Router2------->Router3---------->PC2	
	
	PC1 will encapsulate the IP Packet in Ethernet
		Ethernet Header | IP Packet | Ethernet Trailer
	
	Router1 will extract the IP Packet and encapsulate in HDLC. It is ok to 
	say that a leased line exists between PC1 and Router1
		HDLC header | IP Packet | HDLC trailer
	
	Router2 will extract the IP Packet and encapsulate in
	Ethernet. An EoMPLS service exists between Router 2 and 3.
		Ethernet Header | IP Packet | Ethernet trailer
		
	
	Router 3 will extract the IP packet and encapsulate in new Ethernet
		Ethernet header | IP Packet | Ethernet trailer
		
	PC2 will receive the IP packet.
	
	Routers build new data link headers and trailer because the new headers 
	contain data-link addresses; the PCs and routers must have a way of 
	deciding what data-link addresses to use.
	An example of how the router determines which data-link address to use 
	is the IP Address Resolution Protocol. For instance, Router 3 will use
	ARP to learn about the MAC address of PC2 before sending any packets.
	
	Path selection: sometimes used to refer to the routing process or routing
	protocols, specifically how routing protocols select the best route among 
	competing routes to the same destination.
		
---- What has already been covered:
	* The process of routing of L3PDU based on the destination layer 3
	address in the packet
	
	* The routing process uses the data link layer to encapsulate 
	L3PDU into layer 2 frames for transmission across each successive 
	data link.
		
		
- IP addressing and how Addressing helps IP routing
******************************************************
	IP defines network layer addresses which identify hosts on the router 
	interface that connects to the TCP/IP network.	
		
	Any interface that expects to receive IP packets needs an IP address.

	TCP/IP groups IP addresses together so that IP addresses on the same 
	physical network are part of the same IP address group called an IP 
	network or an IP subnet.
	
	Numerically, addresses of the same IP network have the same value in the
	first part of their address.
	
	A router can list one routing table entry for each IP network or
	subnet,instead of one entry for each IP address.
	
	The routing process also makes use of the IPv4 header which lists a
	32 bit source IP address, as well as a 32 bit destination IP address 
	and other fields; 20bytes in total.
	
	4 bytes of the IPv4 header
	***************************
	Version | Length | DS Field | Packet length
	Identification | Flags | Fragment Offset
	Time to Live | Protocol | Header Checksum
			Source IP address
			Destination IP Address	
			
- Routing protocols
*************************
	For routing to work, both hosts and routers need to know smth abt the TCP/IP internetwork; hosts will require to know the IP address of the default gateway/router so that they can send packets to remote destinaions.
	Routers however need to know routes so that routers know how to forward packets to each and every IP network and IP subnet.
	
	A network engineer could configure(type) all the required routes on every router but mostly they would instead simply enable a routing protocol on all routers. Routers will then send routing protocol messages to each other hence learning the routes for all IP networks and subnets in the TCP/IP internetwork.
	
- IPv4 Addressing
**********************
Key focus--> IPv4 Addressing and subnetting!!
How IP addressing relates to IP routing.

- Rules for IP Address
************************
	IP host, is any device that has at least one interface with an IP address
	that can send and receive IP packets.
	
	IP address consist of a 32 bit number, usually written in Dotted Decimal
	Notation (DDN), (represented in 8bits).
	
	Range of each octet is between 0 and 255, inclusive.
	
	Each network interface uses an unique IP address.
	
- Rules for grouping IP addresses
************************************
	Original specification for TCP/IP grouped IP addresses into sets of 
	consecutive addresses is called an IP network. The address in a single
	IP network have the same numeric value in the first part of all
	addresses in the network.
	
NB::
	All IP addresses in the same group must not be separated from each other
	by a router.
	
	IP addresses separated from each other by a router must be in different
	groups.
	
	IP addressing relies on all addresses in one IP network or IP subnet 
	being in the same location, specifically on a single instance of a LAN
	or WAN data link.
	
	
- Class A , B and C IP networks
*********************************
	IPv4 address space includes literally 232 different values existing in
	a 32bit number, for more than 4billions different numbers. With DDN 
	values, these numbers include all combinations of the values 0 through
	255 in all four octets.
	
	IP standards first subdivide the entire address space into classes, as
	identified by the value of the first octet.
	
	Network ID is just one reserved DDN value per network that indentifies 
	the IP network. It cant be used by a host as an IP address.
	
	Classful IP network refers to any Class A, B or C network because it is
	defined by the IP address rules.
	
- Classfull network
**************************
	A network addressing architecture used in the internet from 1981 until 
	the introduction of classless inter-domain routing in 1993 (CIDR). Classfull
	network divides the IP address space into 5 address classes by address range.
	
- Introduction to address classes (classfull routing)
*****************************************************
	Network expansion had to be compatible with existing networks and 
	avoid renumbering of the existing networks, where there was to be an 
	expansion the definition of the network number field to include more
	bits, hence allowing more networks to be designated, each potentially
	having fewer hosts.
	
	Previously all existing network numbers  at the time were smaller than
	64 and  only used the 6-least significant bits of the network 
	field. Thus it was possible to use the most significant bits of an 
	address to introduce a set of address while preserving existing network
	numbers in the first 3 classes.
	
	Class A contained all network addresses where the MSB is 0, therefore,
	the network number was given by the next 7bits, hence accomodating
	128 networks including the 0 network and existing IP networks.
	
	Class B was to contain all network addresses where the MSB is 1 & 0.
	The network address was provided by the next 14bits of the address,
	thus leaving 16 bits for numbering hosts on the network 
	(65535 addresses per network).
	
	Class C was defined by the 3 high-order bits set to 1, 1 & 0, 
	designating the next 21 bits to number the networks, with each
	network having 256 addresses.
	
	The leading bit sequence 111, was designated and escape to extended 
	addressing mode and was later subdivided as class D (1110) for
	multicast addresing and 1111 for class E which is used for experimental
	purposes.
	
	
	Class A:
		Leading bits: 0
		Size of network field: 8
		Size of the rest bit field: 24
		Number of networks: (2^7) 128
		Addresses per network: 16,777,216
		Total address in class: (2^31) 2,147,483,648
		Start address: 0.0.0.0
		End address: 127.255.255.255
		Default subnet mask in DDN: 255.0.0.0
		CIDR: /8
	
	Class B:
		Leading bits: 1 0
		Size of network field: 16
		Size of the rest bit field: 16
		Number of networks: (2^14) 16,384
		Addresses per network: 65,535
		Total address in class: (2^30) 1,073,741,824
		Start address: 128.0.0.0
		End address: 191.255.255.255
		Default subnet mask in DDN: 255.255.0.0
		CIDR: /16
		
	Class C:
		Leading bits: 1 1 0
		Size of network field: 24
		Size of the rest bit field: 8
		Number of networks: (2^21) 2,097,152 
		Addresses per network: (2^8) 256
		Total address in class: (2^29) 536,870,912
		Start address: 192.0.0.0
		End address: 223.255.255.255
		Default subnet mask in DDN: 255.255.255.0
		CIDR: /24
		
	Class D:
		Leading bits: 1 1 1 0
		Size of network field: N/A
		Size of the rest bit field: N/A
		Number of networks: N/A
		Addresses per network: N/A
		Total address in class: (2^28) 268,435,456
		Start address: 224.0.0.0
		End address: 239.255.255.255
		Default subnet mask in DDN: N/A
		CIDR: N/A
		
	Class E:
		Leading bits: 1 1 1 1
		Size of network field: N/A
		Size of the rest bit field: N/A
		Number of networks: N/A
		Addresses per network: N/A
		Total address in class: (2^28) 268,435,456
		Start address: 240.0.0.0
		End address: 255.255.255.255
		Default subnet mask in DDN: N/A
		CIDR: N/A	
	
	Number of addresses usable for address specific hosts in each network 
	is always 2^N - 2, where N is the number of rest field bits; subtraction
	of 2 adjusts for the use of all-bits-zero for the network address and
	all-bits-one for the broadcast address.
	
	127.0.0.0/8 is assigned for loopback.
	
	
	Class A
  0.  0.  0.  0 = 00000000.00000000.00000000.00000000
127.255.255.255 = 01111111.11111111.11111111.11111111
                  0nnnnnnn.HHHHHHHH.HHHHHHHH.HHHHHHHH

Class B
128.  0.  0.  0 = 10000000.00000000.00000000.00000000
191.255.255.255 = 10111111.11111111.11111111.11111111
                  10nnnnnn.nnnnnnnn.HHHHHHHH.HHHHHHHH

Class C
192.  0.  0.  0 = 11000000.00000000.00000000.00000000
223.255.255.255 = 11011111.11111111.11111111.11111111
                  110nnnnn.nnnnnnnn.nnnnnnnn.HHHHHHHH

Class D
224.  0.  0.  0 = 11100000.00000000.00000000.00000000
239.255.255.255 = 11101111.11111111.11111111.11111111
                  1110XXXX.XXXXXXXX.XXXXXXXX.XXXXXXXX

Class E
240.  0.  0.  0 = 11110000.00000000.00000000.00000000
255.255.255.255 = 11111111.11111111.11111111.11111111
                  1111XXXX.XXXXXXXX.XXXXXXXX.XXXXXXXX
	
	
- Classless Inter-Domain Routing
**********************************
	Introduced as a replacement for Classfull networks.
	
	Main goal was to slow the growth or routing tables on routers across
	the internet and help in slowing the rapid exhaustion of IPv4 addresses.
	
	It allocates address space to ISPs and end users on any address bit 
	boundary, instead of on 8-bit segments like in classfull networks.
	In IPv6, however, the interface identifier has a fixed size of 64 bits
	by convention and smaller subnets are never allocated to end users.
	
	CIDR is encompassed on Variable Length Subnet Masking (VLSM) technique
	which allows a network to be divided into variously sized subnets,
	providing the opportunity to size a network for local needs. RFC 950.
	
	CIDR notation > method of representing IP addresses, in which an address
	or routing prefix is written with a suffix indicating the number of bits
	of the prefix,eg 192.168.2.0/24 for IPv4 and 2001:db8::/32 for IPv6.
	The decimal number represents the number of leading 1 bits in the routing
	mask/ network mask.
	
	The number of addresses within a subnet may be calculated as 
	2^address length - prefix length, in which the address length is 128
	for IPv6 and 32 for IPv4.
	eg in IPv4 the prefix length /29 gives:
	2^32-29 = 2^3 = 8 addresses.
	
- Subnetting
**************
	Defines the methods of further subdividing the IPv4 address space into
	groups that are smaller than a single IP network.
	
	CIDR introduced an administrative process of allocating address blocks 
	to organizations based on their actual and short-term needs.
	
	
- Summary of the router forwarding logic
*****************************************
	Step 1:
		Use the data link Frame Check Sequence (FCS) field to ensure that
		the frame had no errors; if errors occurred, discard the frame.
	
	Step 2:
		Assuming that the frame wasn't discarded step 1, discard the old data
		link header and trailer, leaving the IP packet
		
	Step 3:
		Compare the IP packet's destination IP address to the routing 
		table and find the route that best matches the destination address.
		This route identifies the outgoing interface of the router and
		possibly the next hop router IP address
	
	Step 4:
		Encapsulate the IP packet inside a new data-link header and trailer
		appropriate for the outgoing interface and forward the frame.
		
To match a routing table entry, a router thinks like this:
	Network numbers and subnet number represent a group of addresses that
	begin with the same prefix. Think about those numbers as groups
	of addresses. In which group does the destination
	address of this packet belong to?
	
	
- IPv4 Routing protocols
************************
	Routing process depends heavily on having an accurate up-to date IP 
	routing table on each router. 
	
	Goals of a routing protocol:
		Dynamically learn and fill routing tables with a route to each
		subnet in the subnetwork.
		
		If more than one route to a subnet is available, place the best route.
		
		If a route is removed from the routing table and another route 
		through another neighbouring router is available, add the route
		to the routing table.
		
		The time interval between loosing the route and finding a working
		To work quickly when adding new routes or replacing lost routes
		replacement route is Convergence time.
		
		To prevent routing loops.
