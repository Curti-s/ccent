- Chapter 3
************
- Fundamentalsof WANs
**************************
	Topics covered:
		1.0 Network fundamentals
		1.1 Compare and Contrast OSI and TCP/IP models
		1.6 Select the appropriate cabling type based on the implementation requirements
		3.0 Routing technologies
		3.1 Describe the routing concepts.
		3.1c Frame rewrite

Most layer 1 and 2 technologies fall into one of two primary categories:
	* WAN
	* LAN
Becasue both LANs and WANs have many similarities:
	* both define:
		> cabling details (UTP, TP)
		> transmission speeds.
		> encoding
		> how to send data over physical links as well as
		> data-frames and forwarding logic.
Big difference between LAN and WAN:
	you pay and own LAN, but you lease WAN.

This chapter covers WANs in 3 diff sections:

	* Leased line WANs: a type of WAN link that has been part of the enterprise networks since 1960s.
	
	* How Ethernet can be used to create WAN services by taking advantage over the longer cable length possibilities of mordern fibre-optic Ethernet standards.
	
	* Survey of common WAN technology used to access the Internet.
	
- Do I Know This Already?
******************************
	1.In the cabling for a leased line, which of the following typically connects to a four-wire line provided by a teclo?
	????
	
	a. Router serial interface without internal CSU/DSU
	b. CSU/DSU
	c. Router serial interface with internal transceiver
	d. Switch serial interface	
	
		Channel Service Unit/Data Service Unit, connects to a four wire pair from a Telco, then using a serial DTE cable it connects to a router's serial interface.
		
	2.Which of the following is an accurate speed at which a leased line can operate in the US?
	a. 100 Mbps
	b. 100 Kbps
	c. 256 Kbps
	d. 6.4 Mbps
	
		256Kbps. Between 6.4 Kbps and 1.544 Mbps.
	
	3.Which of the following fields in the HDLC header used by Cisco router does CIsco add, beyond the ISO standard HDLC?
	????
	a. Flag
	b. Type
	c. Address
	d. FCS
		Type. Cisco uses a proprietary HDLC that has a Type implied within the Ethernet frame.
		Flag, Destination Address, Control, Type, Data, FCS
		
	4.Two routers, R1 and R2, connect using an Ethernet over MPLS service (EoMPLS). The service provides point-to-point service between these two routers only, as a layer2 Ethernet service. Which one of the following are most likely to be true about this WAN? (2 answers)
	?????
	a. R1 will connect to a physical Ethernet link, with
	the other end of the cable connected to R2.
	b. R1 will connect to a physical Ethernet link, with
	the other end of the cable connected to a device at
	the WAN service provider point of presence.
	c. R1 will forward data-link frames to R2 using an
	HDLC header/trailer.
	d. R1 will forward data-link frames to R2 using an
	Ethernet header/trailer.
		R1 will connect to a physical Ethernet link, with the other end of the cable connected to a device at the WAN service provider point of presence.
	
		R1 will forward data-link frames to R2 using an Ethernet header/trailer.
	
	5.Which of the following Internet access technologies, used to connect a site to an ISP, offers asymmetric speeds?
	?????
	a. Leased lines
	b. DSL
	c. Cable Internet
	d. BGP
	
		DSL and Cable Internet. This means that there are faster downstream(data transmission from the ISP to the customer) compared to upstream( data transmission to the ISP). Assymetric speeds work much better for consumer internet access from home, because clicking a webpage sends afew hundred bytes upstream but can trigger the delivery of many megabytes of data downstream.
	
	6. Fred has just added DSL service at his home, with a separate DSL modem and consumer-grade router with four Ethernet ports. He wants to use the same old phone he was using before the installation of DSL. Which is most likely true about the phone cabling and phone used with new DSL installation?
	????
	a. He uses the old phone, cabled to one of the
	router/switch device’s Ethernet ports.
	b. He uses the old phone, cabled to the DSL
	modem’s ports.
	c. He uses the old phone, cabled to an existing telephone port and not to any new device.
	d. The old phone must be replaced with a digital
	phone.
		He uses the old phone, cabled to an existing telephone port and not to any new device.
	
	Answers
	1 B 2 C 3 B 4 B and D 5 B and C 6 C
	
	By the end of this chapter I will have the answers to these questions.......
	
- Leased-line WANs
*******************
	From a basic point, a leased line WAN works alot like an Ethernet crossover cable connecting 2 routers, but with few distance limitations. However each router can send at anytime > (full duplex) over the leased line for tens, hundreds or even thousands of miles.
	Main goal of WAN is to move data between LANs.
	
-- Story
	You are the primary network engineer for an enterprise network. The company is building a new site 100miles away from the corporate hq. Of course the new building requires a new remote LAN network which will eventually need to be connected to the existing enterprise TCP/IP network. Therefore, a WAN is required. At a minimum, the WAN must be able to send data from the remote LAN back to the rest of the network and viceversa. Leased line WAN forward data between 2 routers.

- Positioning Leasedlines with LANs and Routers.
*************************************************
	Vast majority of end-user devices in the enterprise/SOHO network connect directly to the LAN using an Ethernet NIC. More devices too support  wireless LAN. eg phones and tablets, laptops etc..
	To connect LANs using a WAN, the internetwork uses a router connected to each LAN, with a WAN link between the routers.
	The world of WAN technologies includes many different options in addition to the crooked line -----/------- which i am familiar with. It includes a large number of physical links as well as data-link protocols that control those links.
	By comparison, wired LAN world basically has one option > Ethernet.
	
- Physical details of leased lines
************************************
	Leased lines conceptually act like full-duplex crossover Ethernet link between two routers. It uses 2 pairs of wire, one pair for each direction of sending data, hence allowing full-duplex communication.
	To create such possibly long leased line links, or circuits, it doesn't actualy exist as a single long cable between the two sites. Instead a telco installs a large network of cables and specialized switching devices to create its own computer network that acts as crossover cable between two points.
	
	NB:: Telco - Telephone Company.
	Leased line : similarly to service provider.
	
	Names used in telco terminology
	********************************
	Name | Meaning/Reference
	-----|--------------------
	Leased circuit, Circuit | Line and Circuit are oftenly used as synonyms in telco terminology, Circuit makes reference to the electrical circuit  between 2 endpoints.
	
	Serial link, Serial line | Line and Link are oftenly used as  synonyms. Serial refer to the fact the bits flow serially between 2 endpoints & that routers use serial interfaces.
	
	Point-to-point link/line | Refers to the fact that a topology stretches between 2 points & 2 points only.
	
	T1 | Specific type of leased line transmitting at 1.544 Mbps
	
	WAN link/line | General terms with no reference to any specific technology.
	
	Private line | Refers to the fact that data sent to a line cannot be copied by other telco customers; data is private.
	
	NB::
		Serial communication not clear..?/#
		Explanation
			The process of sending data one bit at a time, sequentially over a communication channel or computer bus which is in contrast with parallel communication where
			several bits are sent as a whole on a link with several parallel channels. 
			For serial communication, the Most Significant Bits are sent first then the Least Significant bits follow, unlike in parallel where all bits are sent as a whole on
			separate parallel channels.
			Serial communication is used for long-haul communication where cost of cabling and synchronization make it impractical to implement parallel communication.
			
			
			
- Leased line cabling
***********************
	Some physical path must exist between 2 routers on the end links.
	However, a telco doesn't install only 1 cable between the 2 buildings. Instead it uses what is typically a large and complex network that creates an appearance of a cable between the two routers. Telcos install their equipment in buildings called Central Offices (CO), then install their cables from the CO to almost every other building in the city, expecting to sell services to the people in those buildings one day. The Telco will then configure its switches to  use some capacity on each cable to send data in both directions, creating the quivalent of a crossover cable between two routers.
	First, each site has a Customer Premise Equipment (CPE) which includes a router, serial interface card and (CSU/DSU) Channel Service Unit/Data Service Unit. Routers contain NICs for sending data over a physical link. The physical link requires a function called Channel Service Unit/Data Service Unit which can either be intergrated into the serial interface card in the router or sit outside the router as an external device.
	Short serial cables are used to connect the router to the CSU/DSU, typically using RJ-48 connectors. The serial cables are called Data Terminal Equipment (DTE) cables with a male connector. To create a WAN link, you require 2 serial cables, one serial DTE and a similar but slightly different matching (DCE) Data Communication Equipment cable using a female connector. The DCE cable swaps the transmitter and reciever hence acting as a straight-through cable.
	Finally,the router with DCE cable installed needs to do one function, which is normally done by the CSU/DSU; **clocking**, in which it tells the router when exactly to send each bit through signalling over the serial cable.
	Regardless of whether a router is of newer or older version, I will want to know how to configure clocking using the **clock rate** command.	
	
- Data-link Details of Leased Lines
*************************************
	Leased line provides Layer 1 service / transmission of bits. However it doesn't define data link layer protocols to be used.
	Therefore many companies/standard orgs have created data-link protocols to control and use leased lines.
	Most popular protocols:
		* High-Level Data Link Control (HDLC)
		* Point-to-Point Protocol (PPP)
		
- HDLC Basics
*****************
	All data link layer protocols perform similar roles: controlling the correct delivery of data over a physical link. eg Ethernet data-link protocol uses a destination address field to identify the correct device that should receive data and an FCS field that allows receiving device to determine whether the receving data arrived correctly. HDLC provides the same.
	
	HDLC fields and functions:
		Flag
			> Preamble
			> SFD
			> Lists a recognizable bit pattern so that the receiving nodes realize that a new frame is arriving
			
		Address
			> Destination Address
			> Identifies the destination device
			
		Control
			> 
		Type
			> Identifies the type of layer 3 packet encapsulated inside the frame
			
		FCS
			> Used for error detection
			
HDLC exist because of the International Organization for Standardization (ISO). However ISO standard HDLC doesn't have a type field and routers need to know the type of the packet of a frame. Therefore, CISCO routers use a proprietary HDLC version which adds a Type field.
	Flag | Address | Control | Type | Data | FCS
	
	
- Ethernet as a WAN technology
*********************************
	Ethernet was only appropriate for LANs due to restrictions on cable length and the devices that might allow a LAN that stretched a kilometer or 2.
	Improvements by IEEE saw Ethernet being a reasonable WAN technology. eg 1000BASE-LX standard uses single-mode fiber cabling with support for 5 km cable length; 1000BASE-ZX standard supports even longer 70 km cable length.
	
	eg
		CPE ----(fiber ethernet access link)---> Service Provider(Ethernet WAN service) (Point of Presence)

A customer will connect to the Ethernet link using a router interface.
The fiber Ethernet link leave the Customer Site and connects to some SP location called a Point of Presence.

- Ethernet as a WAN technology
**********************************
Focus on the one Ethernet WAN service: Ethernet emulation or Ethernet over MPLS (EoMPLS).
	Ethernet emulation is a general term meaning that the service acts like one Ethernet link.
	EoMPLS > Multiprotocol Label Switching; one of the technologies used within the SP's cloud.

The type of EoMPLS service covered, gives a customer an Ethernet link between two sites; it provides the following;
	* a point-to-point connection between 2 customer devices
	* behaviour as if a fiber Ethernet link existed between the 2 devices.
	
- How routers route IP packets using Ethernet Emulation
********************************************************
	General nature of WAN is to give IP routers a way to forward IP packets from one LAN to another. Routing over an EoMPLS WAN link still uses the WAN like WAN, as a way to forward packets from one site to another, while using the same Ethernet protocols as the Ethernet WAN links at each site.
	EoMPLS link uses Ethernet for both layer 1 and layer 2 functions. i.e same format of Ethernet header and trailer but diff details.
	
	PC1----------> Switch-------> Router1(G0/1(LAN 1))--------##(EoMPLS WAN)##--------->Router2(G0/0(LAN 2))------->Switch-------->PC2
NB::
	##(EoMPLS)## denotes that this Ethernet link uses an Ethernet WAN service.
	Routing steps:
		1.PC1 encapsulates the IP packet to R1 in an Ethernet Frame that has the destination MAC address of R1
		2.R1 de-encapsulates  the IP packet from the Ethernet Frame and encapsulates it into a new Ethernet frame with a new Ethernet header and trailer. 
		The destination MAC address is R2 G0/0 MAC address and the source is R1 G0/1 MAC address.
		3.R2 de-encapsulates the IP packet from the Ethernet frame, encapsulates the packet into a new Ethernet frame with destination MAC address of PC2.	
	
	NB::
		Ethernet over MPLS and DSL do not replace Leased lines in any way as WAN technologies but play an important role in specific case of creating a WAN connection between a home or office and the internet.

- Accessing the Internet
**************************
	 Digital Subscriber Line and cable.
	 Internet as a large WAN or large TCP/IP network including many LANs as it spans the globe. Of course it needs WAN links to connect different sites.
	 The internet includes almost every enterprise and home networks as well as a huge number of individuals from their phones and other wireless devices.
	 At the middle of the internet is called the Internet Core, there exists LANs and WANs owned and operated by ISPs.
	 Alot of WAN links are used, which are better known as **Internet Access Links**.
	Types of Internet Access Links::
		* Leased lines
		* DSL (analog telephone lines)
		* Cable (CATV)
		
	DSL supports assymetrical speeds, meaning, the transmission speed from the ISP towards the home(downstream) is much faster than the transmission towards te ISP(upstream).
	
- DSL
********
	Digital Subscriber Line -> relatively short high-speed WAN between a telco customer and an ISP. It uses telephone line which terminates at RJ-11 ports.
DSLAM > DSL Access Multiplexer. It splits out the data over to the router and voice signals over to the voice switch
	Review topics:
		- Typical diagram for CPE for a leased line
		- Ethernet over MPLS physical connection
		- Common Internet access links
		- Typical DSL cabing at home
		- Typical cable internet cabling at home
	
