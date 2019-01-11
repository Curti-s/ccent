- Chapter 2
***************
## Fundamental of Ethernet LANs

	- Covers the following exam topics
		1.0 networking fundamentals
			1.6 Select appropriate cabling type based on implementation requirements.
		2.0 LAN Switching Technolgies
			2.1 Describe and verify the switching concepts
			2.1.a MAC learning and aging
			2.1.b Frame switching
			2.1.c Frame flooding
			2.1.d MAC address table
			2.2 Interpret Ethernet frame format

Many types of LANs have existed over the year, but today's networks use two general types od LANs:
	* Ethernet LAN
	* Wireless LAN
Ethernet LAN happen to use cables for the links between nodes, oftenly called wired LANs

- Do I Know This Already?
-----------------------------
1. In the LAN for a small office, some user devices connect to the LAN using a cable, while other connect using wireless technology.Which of the following us true regarding the use of Ethernet in this LAN?
	
	Only devices that are using cables are using Ethernet.

2. Which of the following Ethernet starndards defines Gigabit Ethernet over UTP cabling?
	
	10000Base-T
	
3. Which of the following is true about Ethernet crossover cables for FastEthernet?
	
	Pins 1 and 2 on one end of the cable connect to pins 3 and 6 on the other end of the cable.
		Endpoints receive and transmit on the same pins
		The crossover cable pinout crosses the pair at the transmit pins on each device
		to the recieve pins on the opposite device.
		Switches transmit on the pair at pins 3 and 6 and both receive on the pair
		at pins 1 and 2.
	
4. Each answer lists two types of devices used in a 100BASE-T network. If these devices were connected with UTP Ethernet cables, which pairs of devices would require a straight-through cable?
	
	PC and Router
	PC and Switch
	
5. Which of the following is true about CSMA/CD algorithm?
	
	Collisions can happen, but the algorithm defines how the computers should notice a collision and how to recover.
	
6. Which of the following is true about Ethernet FCS field?
	
	???? -> Resides in the Ethernet trailer, not the Ethernet header.
	
7. Which of the following are true about the format of Ethernet addresses?
	
	Each manufacturer puts a unique OUI code into the first 2 bytes of the address.
	Each manufacturer puts a uique OUI code into the first half of the address.
	Ethernet address is 6 bytes/48bit long / 12 digit hexadecimal number. Often
	calle **unicast** ethernet address.
	
	
8. Which of the following terms describe Ethernet address that can be used to send one frame that is delivered to multiple devices on the LAN?
	
	Broadcast address and Multicast address.
	
	
	
	
Ethernet refers to a family of LAN standards that together define the physical and data link layers of the worlds most popular wired LAN technology.
The standards defined by IEEE include: cabling - type / length, connectors on the ends
of cables, protocol rules, speed  etc

- Typical SOHO LANs
*************************
	First the LAN requires a device called an Ethernet LAN switch, which provides many physical ports.
	The router connects the LAN to a WAN(internet). However, SOHO 	Ethernet LANs today combine the router and switch into a single device.
	Typical SOHO LANs support wireless LAN connections that use wireless LAN technology defined by IEEE, that begin with 802.11 and use radio waves to send bits from one node to the next.
	Most wireless LAN rely yet on another networking device: Wireless Access point, that acts somewhat as an Ethernet switch. It only requires Ethernet ports for connecting the AP to the Ethernet LAN.
	
	
- Typical Enterprise LANs
****************************
	For instance conceptionally, an enterprise may contain a number of floors, with each having a switch that connects to one distribution switch which in turn connects to the router that routes information to the internet.

----------- IEEE 802 Standards-----------------
************************************************
	IEEE 802 is a family of standards dealing with LAN and MAN networks.More specifically IEEE 802 is restricted to  networks carrying variable-size packets.
	NB::
		Cell relay networks, where data is transmitted in uniformly-sized  units called cells.
		Isochronous networks, where data is transmitted in a steady stream of groups of octets, at regular time intervals.
	
	Services and protocols of the IEEE 802 map to the 2 lower layers of the OSI networking reference model. It infact splits the data-link layer into 2 sub-layers: logical link control and media access control.
	Most widely used standards are the Ethernet, Token Ring, Wireless LAN, Bridging and Virtual bridged LANs.
	List of indivual working groups:
		
		IEEE 802.1 Higher Layer LAN Protocols(Bridging) -> active
		IEEE 802.2 LLC -> x 
		IEEE 802.3 Ethernet -> active
		IEEE 802.4 Token Bus -> x
		IEEE 802.11 Wireless LAN -> active
	To view other 802.x standards -> [IEEE 802] (https://en.wikipedia.org/wiki/IEEE_802)
	
- Variety of Ethernet physical layer standards
*************************************************

	Speed	|	Common Name	|	Informal IEEE Standard name	| Formal Standard Name
----------------------------------------------------------------------------------
	10Mbps	|	Ethernet	|	10BASE-T	|	802.3	|	Copper, 100m
	100Mbps	|	FastEthernet| 100BASE-T		|	802.3u	|	Copper, 100m
	1000Mbps|	Gigabit Ethernet |	1000BASE-LX	|	802.3z	|	Fiber, 5000m
	1000Mbps|	Gigabit Ethernet |	1000BASE-T	|	802.3ab	|	Copper, 100m
	10Gbps	|	10 Gig Ethernet	 |	10GBASE-T	|	802.3an |	Copper, 100m


While physical standards focus on sending bits over a cable, data-link layer focuses on sending an Ethernet frame from source to destination ethernet node.

The term frame specifically refers to the header and trailer of a data-link protocol plus the data encapsulated inside the header and trailer.

- Demistifying UTP Ethernet link
*************************************
	Ethernet link refers to any physical cable between 2 Ethernet nodes. UTP cable holds copper wires grouped as twisted pairs.
	10BASE-T(802.3) and 100BASE-T(802.3u) standards require 2 pairs, whereas 1000BASE-T(802.3ab) standard requires 4 wire pairs.
	Many Ethernet UTP cables use an RJ-45 connectors on both ends; it has 8 physical contacts.
	
	NB::
		SFP+ transceiver - > Small Form-Factor Pluggable receiver

- Straight-Through Cable pinout for 10BASE-T and 100BASE-T
***********************************************************
	Connecting a PC to a LAN switch.
	Understand how NICs and switches work:
		As a rule, Ethernet NIC transmitters use a pair connected to pins 1 & 2; the Ethenet receivers use a pair of wires at positions 3 and 6. LAN switches, knowing those facts abt the Ethernet NICs, do the opposite; the receivers use the wire pair at pins 1 & 2, and their transmitters use the wire pair at pins 3 & 6.
	A straight-through cable works correctly when the nodes use opposite pairs for transmitting data.
	
- Crossover Cable Pinout for 10BASE-T and 100BASE-T
*******************************************************
	It crosses the pair at the transmit pins on each device to the receive pins on the opposite device.
	2 switches will both transmit at pins 3 and 6 and receive on the pair pins at 1 & 2.
	
	
	NB::
		Cisco switches have a feature called auto-mdix that notices when the wrong cabling is used and automatically changes its logic to make the link work.
		
- UTP Cabling pinouts for 1000BASE-T
****************************************
	Gigabit Ethernet differs from Ethernet and FastEthernet as far as cabling and pinouts are concerned. First it requires 4 wire pairs. Second it uses more advanced electronics that allow both ends to transmit and receive simulataneously on each wire pair.
	
	

- Ethernet  Data Link Protocols
***********************************
	It defines the Ethernet frame: comprising of :
		* Ethernet header
			- Preamble 
				> 7 bytes
				> Synchronization
				
			- SFD
				> Start Frame Delimiter
				> 1 byte
				> Signifies that the next byte begins the Destination MAC address field.
				
			- Destination MAC address
				> 6 bytes
				> Identifies the intended recepient of this frame
				
			- Source MAC address
				> 6 bytes
				> Identifies the sender of this frame
				
			- Type
				> 2 bytes
				> Defines the type of protocol listed in the frame; most likely identifies the IP version(4/6)
				
			
		* Encapsulated data
			> 46 to 1500 bytes
			> Holds data from a higher layer, typically L3PDU (usually a IPv4 or IPv6 packet).
			
		* Ethernet trailer
			> 4 bytes
			- FCS Frame Check Sequence
			> Provides a method for receiving NIC to determine whether the frame experienced transmission errors.
			
			
	NB::
		The IEEE 802.3 limits the data portion of the 802.3 frame to a minimum of 46 bytes and a  maximum of 1500bytes. The term (MTU) Maximum Transmission Unit defines the max Layer 3 packet that can be sent over a medium, because it rests inside the data portion of an Ethernet frame.

- Ethernet Address
********************
	General idea:
		The sending node puts its own address in the source address field and the intended Ethernet destination device's address in the destination address field. The sender transmits the frame, expecting that the Ethernet LAN, as a whole will deliver the frame to the correct destination.
		Ethernet Address -> Media Access Control:
			6-byte long(48bits) binary number.
			Conviniently listed as a 12-digit hexadecimal.
		Most MAC addresses represent a single NIC or other Ethernet port, therefore they are often called unicast Ethernet addresses. i.e single interface of the Ethernet LAN.
		
		Other names for Ethernet addresses:
			* LAN address
			* Hardware address
			* Burned-in address
			* Physical address
			* Universal address
			* Global MAC address
			* Unicast address
	In addition to unicast addresses, Ethernet also uses group addresses to identify more than one LAN interface card. A frame sent to a group address might be delivered to a small set of devices on the LAN or to all devices.
	Categories of group addresses defined by IEEE:
		* Broadcast address
			- Frames sent to this address should be delivered to all devices on the Ethernet LAN. Has a value of FFFF.FFFF.FFFF
			
		* Multicast address
			- Frames sent to multicast Ethernet address will be copied and forwaded to a subset of the devices on the LAN that volunteers to receive frames sent to a specific multicast address.
			Multicast addresses will have a value of 1 in the least significant bit of the first octet  of the destination address, thus helping the network to distinguish btwn a multicast and broadcast. Example:
			01:00:CC:CC:CC:CC, which is an address used by Cisco Discovery Protocol (CDP).
	
- Identifying Network layer protocols with the Ethernet Type Field
*********************************************************************
	- Ethernet type field / EtherType, sits in the Ethernet data link layer header, but its purpose is to directly help the network processing on routers and hosts. Basically it identifies the type of the network layer (layer 3) packet that sits inside the Ethernet frame.
	Network layer protocols used over the years include:
		* IBM's Systems Network Architecure (SNA),
		* Novell Netware 
		* Digital Equipment Corporation's (DECnet)
		* Apple Computer's AppleTalk
	Most common protocol used: TCP/IP (IPv4/IPv6)
	
	Q. What number should the sender put in the header to identify an IPv4 packet as the type or an IPv6 packet?
	Answer
	*****
	IEEE manages a list of EtherType values, so that every network layer protocol that needs a unique EtherType value can have a number. For instance a  sender can send an Ethernet frame with an IPv4 packet and the next frame with an IPv6 packet; each frame would have a diff Ethernet Type field value. eg 
	IPv4: Ethernet Header | IPv4(Type = 0800) | Ethernet Trailer
	
	IPv6: Ethernet Header | IPv6 (Type = 86DD) | Ethernet Trailer
	
	
- Error Detection with FCS ----Frame Check Sequence-----
*********************************************************
	Ethernet defines away for nodes to find out whether a frame's bit has changed while crossing over an Ethernet link i.e due to electrical interference or bad NIC.
	Frame Check Sequence, found in the Ethernet Trailer.
	The sender applies a complex math formula to the frame before sending it, storing the rest of the formula in the FCS field. The receiver applies the same math formula to the recieved frame & then compares its own results with the sender's results. Similar results indicate that the frame did not change otherwise the frame is dropped when results are not similar.
	NB::
		Error detection doesn't mean Error recovery.
		Ethernet defines that errored frames should be discarded.
- 
- Sending Ethernet frames with Switches and Hubs
***************************************************
	Ethernet LANs behave differently depending on whether there are switches or hubs used. Basically, the use of mordern switches allows the use of full-duplex logic which is much more faster compared to half-duplex logic which is used when using hubs.
	
	- Sending in mordern Ethernet LANs using full-duplex

	 Most Ethernet standards use a variety of Ethernet physical standards, but with
	 standard Ethernet Frames which can flow over these types of physical links. Each
	 link can be running at different speeds, with the process being relatively simple:
	 > the simplicity lets each device send a large number of frames per second.
	Example: PC1 sending to PC2 through switch 1 and switch2.
	
	PC1-----(10BASE-T(full-duplex))-----> SW1-----(G0/1 1000BASE-T (full-duplex))------->SW2-----(F0/2 100BASE-T)------->PC2
	
	Steps:
	1.PC1 builds and sends the original Ethernet frame using its own  MAC address as
	the source address and PC2's MAC address destination address.
	
	2.Switch 1 receives and forwards the Ethernet frame to its G0/1 interface to Switch2
	
	3.Switch 2 receives and forwards the Ethernet frame to its F0/2 interface to PC2
	
	4.PC2 receives the Ethernet frame, recognizes the destination MAC address as its
	own and processes the frame.
	
	- Using Half duplex with LAN Hubs
	********************************
	LAN hubs forward data using physical layer standards and are therefore considered to be layer1 devices. Electrical signals coming through one hub port are repeated out to all other hub ports except the incoming port, therfore data hopefully reaches the correct destination. 
	NB::
		The hub has no concept of Ethernet frames.
	The downside of using hubs, is that if 2 or more devices trasmit data,electrical signals collide and become garbled. The hub will repeat the signals to all ports at the same time,irregardless of them being garbled.
	To prevent collisions in a switch, half-duplex logic is implemented within the nodes while using CSMA/CD.
	The algorithm takes care of obvious cases caused by unfortunate timing. For
	instance, 2 nodes could check for an incoming frame at the same time & realize that
	no other node is sending, then both send their frames at the exact instant,
	causing a collision.
	CSMA/CD covers these cases as well as follows:
	
	Step1 A device with a frame listens until the Ethernet is not busy.
	
	Step2 When the Ethernet is not busy, the sender begins sending the frame.
	
	Step3 The sender listens while sending to discover whether collision occurs; if 
	if occurs, all currently sending nodes do the following:
		- They send a jamming signal to inform all nodes that collision has happened.
		- They independently choose a random time to wait before trying again to avoid 
		unfortunate timing
		- The next attempt starts again at step 1.
	
	Half-duplex - The device must wait to send if it is currently receiving a frame: cannot send and receive at
	the same time.
	
	Full duplex: - The device doesn't have to wait before sending; can send and receive at the same time.
	
- Key Review topics
******************
	* Drawing a typical wirless and wireless enterprise LAN
	* Several types of Ethernet LANs and some details about each
	* Conceptual drawing of transmitting in one direction each over two different
	electrical circuits between two Ethernet nodes.
	* 10 and 100Mbps Ethernet straight-through cable pinouts
	* 10 and 100Mbps crossover cable pinouts
	* List of devices that transmit on wire pair 1,2 and pair 3,6
	* Typical uses for straight-through and crossover cables.
	* Format of Ethernet MAC address
	* Definition of half duplex and full duplex
	* Examples of which interfaces use full duplex and which interfaces use half-duplex.
	
			
