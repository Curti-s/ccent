Part III: Ethernet LANs: Design, VLANs and Troubleshooting
***********************************************************

Chapter 10: Analyzing Ethernet LAN Designs
Chapter 11: Implementing Ethernet Virtual LANs
Chapter 12: Troubleshooting Ethernet LANs

Part III Review
----------------
	Builds on the basics of implementing Ethernet in Part II, by taking the concepts
	of configuration, troubleshooting to another step.
	Understanding how a small LAN with one or two switches works is a great place
	to start, but understanding why an experienced network engineer might build
	a larger LAN a particular way helps you understand  how LANs work in a real 
	network.
	
	VLANs are one of the most powerful design tools for a network designer & have
	a huge impact on how a switch works, which then impacts how you verify and
	troubleshoot the operations of a campus LAN network.
	
	Chapter 11 shows the details of VLAN operations along with VLAN trunking.
	
	The final chapter ends the chapters that focus on Ethernet as well as serving as
	a great review of many of the topics in Part II and Part III.
	
-10 Analysing Ethernet LAN Designs.
***********************************
This chapter covers the following exam topics:
	1.0 Network Fundamentals
	1.3 Describe the impact of infrastructure components in an enterprise network.
	1.3b Access points
	1.3c Wireless controllers
	1.4 Compare and contrast collapsed core and three-tier architectures
	1.5 Compare and contrast network topologies
	1.5a Star
	1.5b Mesh
	1.5c Hybrid
	1.6 Select the appropriate cabling type based on the implementation requirements
	2.0 LAN Switching Technologies
	2.3 Troubleshoot interface and cabling issues.(collisions, errors, duplex, speed)

	Ethernet defines what happens on each Ethernet link but more interesting & more detailed work happens on the
	devices connected to those links: the NIC.

	This chapter takes chapter 2 "Fundamentals of Ethernet LANs" and dives deeply into many aspects of modern 
	Ethernet LAN while focusing on the primary device used to create these LANs: LAN switches.

	This chapter breaks the discussion of Ethernet & LAN switching into 2 major parts:
	-> The first section looks at the logic used by LAN switches when forwarding Ethernet frames along with related 
	terminology.
	-> The second section considers design and implementation issues, as if you were building a new Ethernet LAN
	in a building or campus; considering design issues, including switches of different types of Ethernet links &
	how to take advantage of Ethernet **autonegotiation**.


Do I Know This Already?
*************************
Analyzing Collision Domains and Broadcast Domains
Analyzing Campus LAN Topologies
Analyzing LAN Physical Standard Choices.

1. Which of the following devices would be in the same collision domain as PC1?
	A. PC2, which is separated from PC1 by an Ethernet hub.
	B. PC3, which is separated from PC1 by a transparent bridge.
	C. PC4, which is separated from PC1 by an Ethernet switch.
	D. PC5, which is seperated from PC1 by a router.

	>>
2. Which of the following devices would be in the same broadcast domain as PC1?(CHoose 3 answers)
	A. PC2, which is separated from PC1 by an Ethernet hub.
	B. PC3, which is separated from PC1 by a transparent bridge.
	C. PC4, which is separated from PC1 by an Ethernet switch.
	D. PC5, which is seperated from PC1 by a router.

	>>

3. In a two-dier campus LAN design, whih of the following are typically true of the topology design?
	(Choose 2 answers)
	A. The design uses a full mesh of links between access and distribution switches.
	B. The design uses a partial mesh of links between access and  distribution switches
	C. The  design uses a partial mesh of links between the distribition and core switches
	D. The end user and server devices connect directly to access layer switches

4. In a three-tier campus LAN design, which of the following a re typically  true of the topology design?
	(Choose 2 answers)
	A. The design uses a partial mesh of links between access and  distribution switches
	B. The design uses a full mesh of links between access and distribution switches.
	C. The  design uses a partial mesh of links between the distribition and core switches
	D. The end user and the server directly connect to the distribution layer switches.

5.	Which answer gives  the strongest match between 1 part of a typical three-tier design with the idea behind
	the listed generic topology design term?
	A. The access layer looks like a partial mesh.
	B. The distribution layer looks like a full mesh.
	C. The distribution layer looks like a hybrid design
	D. The access layer looks like a star design.

6. Which of the following Ethernet standards supports a max cable length of longer than 100m? (Choose 2 answers)
	A. 100BASE-T
	B. 1000BASE-SX
	C. 1000BASE-T
	D. 1000BASE-LX

Answers
1 A 2 A, B, C 3 B, D 4 A, C 5 D 6 B, D

By the end of this chapter I'll have the answers to these questions

Foundation topics
------------------

Analyzing Collision Domains and Broadcast Domains
**************************************************

	In order to understand the terms collision and broadcast domains & how they apply to modern LANs, I need to work back
	through the history of Ethernet in a bit.

Ethernet Collision Domains
*******************************

	People new to Ethernet often get confused with the term **collision domain**: as to how  they apply to modern Ethernet, 
	since modern Ethernet LANs are done so properly to prevent collisions.

10BASE-T Hub
************

	Introduced in 1990 & significantly changed the design of Ethernet LANs.
	It introduced the cabling  model similar to today's Ethernet LANs, with each device connecting to a central device,
	using unshielded twisted pair cable. However, [Ethernet Hubs] were used. It reduced cabling costs.

	Although a hub and a switch use the same star cabling topology, a hub doesn't forward frames the same way a switch
	does: they use the physical layer standards. Basically acts as a repeater. It doesn't have to look at the source &
	destination MAC address of the Ethernet frame. When a repeter receives incoming electrical signals, it forwards a 
	regenerated signal out to all other ports except the incoming port with no thought of CSMA/CD. -> Physically 
	sending out a cleaner version of the incoming electrical signals.

	Because a hub doesn't make an attempt to prevent colisions, the devices connected to it sit within the same collision
	domain. A collision domain, is the set of NICs and device ports for which if they sent a frame at the same time,
	the frames will collide.

	Hubs create a physical star topology.

Ethernet Transparent Bridges
*****************************
	From a design perspective, 10BASE-T was a great improvement, however, it had performance issues where, devices had to 
	wait their turn in order to transmit over the network. Perfomance could be improved in the sense that multiple devices
	could be allowed to send at the same time without there beig a collision.
	
	The first method to allow for multiple devices to transmit at the same time was Ethernet transparent bridge / simply 
	bridges.
	Bridges sat between hubs and divided the network into multiple collision domains.
	Bridges increase the capacity of an Ethernet LAN, because each collision domain can have one instance of CSMA/CD, 
	therefore each collision domain having one sender at a time.
	
	A bridge makes forwading decisions like a modern LAN switch: -> predecessor to switches. Like switches, they hold 
	Ethernet frames in memory, waiting to send out the outgoing interfaces based on CSMA/CD rules.
	
Ethernet Switches and Collision Domains
****************************************
	LAN switches perform the same basic core functions as bridges but with much faster speeds and enhancement.
	Switches break collision domains, each with its own capacity & if the network doesn;t have a hub, each single
	link in a mordern LAN is considered its own  collision domain, even if no collisions can occur in that case.
	
	Modern Ethernet LANs, are built with switches but not bridges and hubs. The switches connect to each other and every 
	link is a separate collision domain. As strange as it sounds, each of those links may never have a collision -> devices
	supporting full duplex; therefore we can turn off CSMA/CD.
	
	NB::
		Routers within a network create separate collision domains, because frames entering  or exiting one router LAN
		interface do not collide with frames on another router's LAN interfaces. 
		
		
Impact of collision on LAN Design
*********************************
	
	Long time ago collisions were normal in Ethernet, therefore analysing Ethernet collision domains was important.
	A modern campus LAN using only switches and neither hubs nor bridges, with full duplex links has no collisions at all.
	
	So when do we need think abt collisions? Whenever a port that could use full duplex happens to use half-duplex, by the
	result of autonegations or any other reason, collisions can now occur.
	
	The term collision domain doesn't apply to WAN interfaces.
	
Ethernet Broadcast Domains.
****************************
	
	Broadcast domain is the set of devices to which a broadcast is delivered.
	
	Think abt modern LAN where a broadcast frame flows. Imagine if switches used the default to put all interfaces in VLAN 1.
	As a result, a broadcast frame sent by one device, would be flooded to all devices connected to all switches (except the
	device sending the original frame).
	
	A router doesn't forward LAN broadcasts. Hubs forward electrical signals, without thinking of it as an Ethernet frame.
	Bridges use the same forwarding logic used by a switch.**(flooding)**
	Routers	separate a network into separate broadcast domain.
	
	Broadcasts sent by a device in one broadcast domain are not forwarded to devices in other broadcast domains.
	
	
Virtual LANs
************
	
	Routers create multiple broadcast domains as a side effect of how IP routing works. A network designer may set
	to use multiple router interfaces to create a large number of multiple broadcast domains hence consuming alot of
	router interfaces. 
	
	However, the use of VirtualLANs, a tool intergrated into switches may be very efficient, since it doesn't consume many
	ports. It gives the designer the ability to design the right number of broadcast domains.
	
	To understand VLANs, first appreciate what LANs do: a LAN consists of all devices in the same broadcast domain.
	Switches create multiple broadcast domains by placing interfaces into VLANs. Switch forwarding logic doesn't forward
	frames from one port in one VLAN to a port in another VLAN. Instead, routers must forward packets  between VLANs using 
	the routing logic. Therefore, instead of all ports in a switch forming a single broadcast domain, the switch is configured
	to separate them into many.
	
	
Impact of Broadcast Domains on LAN Design
******************************************

	Modern LANs try to avoid collisions, since they impede performance. However, LANs cannot remove broadcasts because they play
	an important role in many protocols. 
	Therefore, when thinking about broadcast domains, the choices are more of abt tradeoffs rather than designing to remove 
	broadcasts.
	
	For instance, a small number of large broadcast domains can lead to performance problems for the devices in that broadcast.
	Oppositely, a large number of broadcast domains with small number of devices could lead to other problems too.
	
	In large broadcast domain, each host has to process received frames, whereby the NIC interrupts the CPU which it must spend
	time thinking abt the broadcast frame. eg Ip Address Resolution Protocols. (ARP).
	
	The more the devices in a broadcast domain, the more the number of unecessary CPU interruptions.
	Therefore, the size of a VLAn must be considered.
	
	In summary:
		 - Broadcasts exits,so I'll be ready to analyze a design to define each broadcast domain, ie, each set of devices
		   whose broadcasts reach to other devices in  that domain.
		   
		 - VLANs are broadcast domains created through config
		 
		 - Routers since they don't forward Ethernet frames, they separate broadcast domains off their Ethernet interfaces.
		 

Analyzing Campus LAN Topologies
********************************

	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	