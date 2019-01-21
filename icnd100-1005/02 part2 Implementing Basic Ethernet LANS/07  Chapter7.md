- 07 Analyzing Ethernet LAN Switching
****************************************
	Covers the following exam topics:
		2.0 LAN Switching Technologies
		2.1 Describe and verify switching concepts
		2.1a MAC learning and aging
		2.1b Frame switching
		2.1c Frame flooding
		2.1d MAC address table
		

This chapter has 2 major sections:
	- Concept behind LAN switching, which was introduced in chapter 2
	  "Fundamentals of Ethernet LANs"
	  
	- Using IOS show commands to verify that Cisco switches actually learnt the MAC
	  addresses, built its MAC address table and forwarded frames.
	  
	  
	  
Do I Know This Already?
************************

1.	Which of the following statements describes part of the process of how a switch 
	decides to forward a frame destined for a known unicast MAC address?
		
	 A. It compares the unicast destination address to the bridging, or MAC address
	 	table.
	 B. It compares the unicast source address to the bridging or MAC address table
	 C. It forwards the frame out all interfaces in the same VLAN except for the
	 	incoming interface.
	 D. It compares the destination IP address to the destination MAC address
	 E. It compares the frame's incoming interface to the source MAC entry in the
	 	MAC address table.
	 	
	 	
	 >> It compares the unicast destination address to the bridging, or MAC address
	 table.

2.	Which of the following statements decribes part of the process of how a LAN switch 
	decides to forward a frame destined for a **broadcast** MAC address?
	
	 A. It compares the unicast destination address to the bridging, or MAC address
	 	table.
	 B. It compares the unicast source address to the bridging or MAC address table
	 C. It forwards the frame out all interfaces in the same VLAN except for the
	 	incoming interface.
	 D. It compares the destination IP address to the destination MAC address
	 E. It compares the frame's incoming interface to the source MAC entry in the
	 	MAC address table.
	 	
	 >> It forwards the frame out all interfaces in the same VLAN except for the
	 	incoming interface.
	 	
3.	Which of the following best describes what a switch does with a frame destined
	for an **unknown unicast** address?
	
	 A. It forwards out all interfaces in the same VLAN except for the incoming
	 	interface.
	 B. It forwards the frame out the one interface identified by the matching entry
	 	in the MAC address table
	 C. It compares the destination IP address to the destination MAC address.
	 D. It compares the frame's incoming interface to the source MAC entry in the
	 	MAC address table.
	 	
	 >> It forwards out all interfaces in the same  VLAN except for the incoming
	 	interface.
	 
4.	Which of the following comparisions does a switch make when deciding whether a new 
	MAC address should be added to its MAC address table?
	
	 A. It compares the unicast destination address to the bridging,or MAC address
	 	table
	 B. It compares the unicast source address to the bridging or MAC address table
	 C. It compares the VLAN ID to the bridging or MAC address table
	 D. It compares the destination IP address's ARP cache entry to the bridging or
	 	MAC address table
	 	
	 >> It compares the unicast source address to the bridging, or MAC address table.
	 	Learning always occurs by looking at the source MAC address in the frame then
	 	adds the incming interface as the associated port

5.	A cisco catalyst switch has 24 10/100 ports, numbered 0/1 through 0/24. Ten PCs 
	connect to the ten lowest numbered port, with these PCs working and sending data
	over the network. The other ports are not connected to any device. Which of the
	following answers lists facts displayed by the show interfaces status command?
	
	 A. Port Ethernet 0/1 is in a connected state
	 B. Port Fast Ethernet 0/11 is is in a connected state
	 C. Port Fast Ethernet 0/5 is in a connected state
	 D. Port Ethernet 0/15 is in a notconnected state.
	 
	 >>	Port Fast Ethernet 0/5 is in a connected state.
	 	Remember, for interfaces supporting multiple speeds, the fastest speed is 
	 	what is going to be used to identify it. Therefore, it is not right to say
	 	that Port Ethernet 0/1 is in a connected state, because it is of 10/100 speed.
	 	
	 	Keyword **Ethernet** & **Fast Ethernet**


LAN Switching Concepts
***********************
	The first half of this chapter examines the logic: how a switch chooses to
	forward an Ethernet frame & when the switch chooses to not forward the frame.
	
	The role of a LAN switch is to forward Ethernet frames to the correct
	destination MAC address. LANs exist as a set of user devices, servers and other
	devices that connect to switches, with the  switches connected to each other.
	
	To achieve this, switches use logic, based on the source and destination MAC
	address in each frame's Ethernet header.
	
	It performs the following 3 actions:
		-	Deciding when to forward a frame or when to filter(not forward) a frame,
			based on the destination MAC address.
			
		- 	Preparing to forward frames by learning MAC addresses, by examining the
			source MAC address of each frame received by the switch.
			
		- 	Preparing to forward only one copy of the frame to the destination by 
			creating a (Layer 2) loop-free environment with other switches by using
			**Spanning Tree Protocol (STP)**.	
			
			
	Review of the Ethernet frame:
		Header:
			Preamble - 7bytes
			Start Frame Delimiter - 1byte
			Destination address - 6bytes
			Source address - 6bytes
			Type - 2bytes
			
		Data - 46 to 1500 bytes
		
		Trailer
			Frame Check Sequence - 4 bytes
			
Destination and Source MAC address - 6bytes log(represented in 12hex digits).

Forwarding know unicast frames
*******************************
	A switch uses a dynamically built table that lists MAC addresses and outgoing 
	interfaces to decide whether to forward a frame.
	Switches compare the frame's destination MAC address to this table to decide 
	whether the switch should  forward a frame or ignore it.
	
	example of MAC address table
	
	MAC Address           Output
	----------------     ------------
	0200.1111.1111        F0/1
	0200.2222.2222        F0/2
	0200.3333.3333        F0/3
	0200.4444.4444        F0/4
	
	
	Switch MAC address table also known as **Switching table / Bridging table** or 
	even **Content-Addressable Memory (CAM)**. 
	For LANs with multiple switches, each switch makes independent forwarding decisions
	based on its own MAC address table.
	
Learning MAC addresses
**********************
	Switches do their second main function: learning MAC addresses and interfaces
	to put into their address table. With a complete MAC address table, the switch 
	can make accurate forwarding & filtering decisions.
	
	Switches build the address table by listening to incoming frames and examining
	the source MAC address in the frame.
	
	If a frame enters a switch, and the source MAC address is not in the MAC address
	table, the switch creates an entry in the table, listing the interface from which
	the frame arrived.
	
	NB:
		The table entry lists the interface from which the frame arrived.
		Learning always occurs by looking at the source MAC address in the frame
		and adding the incoming interface as the associated port.
	
Flooding unkown unicast and broadcast frames
*********************************************
	When a frame enters a switch and it happens there are no matching entries in the 
	table, the switch forwards the frame out to all interfaces except the incoming 
	interface, using a process called **flooding**.
	
	A frame whose destination address is unkown is called a **unknown unicast frame**
	or simply **unknown unicast**.
	
	Switches flood unknown unicast frames. Idea is, if you do not know where to send,
	send it everywhere... to deliver the frame and by the way, that device will 
	likely send a reply & the switch will learn its MAC address & forward future 
	frames out to that one port.
	
	Switches also flood LAN **broacast frames** (frame destined to the Ethernet
	broadcast address of **FFFF.FFFF.FFFF**), because this helps to deliver the 
	frame to all device in the LAN.
	
Avoiding  Loops using Spanning Tree Protocol
*********************************************
	Third primary feature of LAN switches is loop preventions, as implemented by
	Spanning Tree Protocol. Without STP, any flooded Frames would loop for an 
	indefinite period of time in Ethernet networks with physical redundant links.
	
	To prevent looping frames, STP blocks some ports from forwarding frames so
	that only one active path exists between any pair of LAN segments.
	
	However, STP has negative features as well, including the fact that it takes 
	some work to balance traffic across redundant alternate links.
	
	Flooding of an unkown unicasts is good mechanism for forwarding unknown unicasts
	& broadcasts, however the continual flooding of traffic frames will continually 
	congest the LAN to the point of making it unusable.
	
	A topology of redundant links is good, but we need to prevent the bad effect
	of those looping frames, whereby STP is used; causing each interface on a switch
	to settle into either **blocking state** or **forwarding state**.
	
	Blocking means that the interface cannot receive or forward data.
	Forwarding means that the interface can send and receive data.
	
	If a correct subset of interfaces is blocked, only single currently logical
	paths exist between each pair of LANs.
	
	NB::
		STP behaves identically for a transparent bridge and switch. Therefore the
		terms bridge, switch and bridging device all are used interchangeably when
		discussing STP.
		
LAN switching summary
***********************
	Switches use layer 2 logic; examining Ethernet data-link header to choose how
	to process frames.
	
	In particular, switches make decisions to forward and filter frames, learn MAC 
	addresses and use STP to avoid loops as follows:
	
		Step 1:
			Switches forward frames based on the destination MAC address:
				A.	If the destination MAC address is a broadcast, multicast
					or unknown destination unicast, the switch floods the frame.
					
				B.	If the destination MAC address is known unicast address:
						
						(i). If the outgoing interface listed in the MAC address
							is different from the interface in which the frame was
							received, the switch forwards the frame out the outgoing
							interface.
							
						(ii).If the outgoing interface is the same as the interface
							in which the frame was received, the switch filters the 
							frame, meaning that the switch simply ignores the frame
							and doesn't forward it.
		Step 2:
			Switches use the following logic to learn MAC address table entries:
				A.	For each received frame, examine the source MAC address 
					and note the interface from which the frame was received.
				
				B.	If it is not already in the table add the MAC address and 
					interface it was learnt on.
					
		Step 3:
			Switches use STP to prevent loops by causing some interfaces (redundant) to block,
			meaning that they neither send nor receive frames.
			
Verifying & Analyzing Ethernet Switching
*****************************************

	Cisco Catalyst switches come ready to get busy switching frames because of 
	default settings like as follows:
		
		-	Interfaces are enabled by default, ready to start working once the 
			cable is connected.
			
		- All interfaces are assigned to VLAN 1.
		
		-	10/100 and 10/100/1000 interfaces use autonegotiation by default.
		
		-	MAC learning, forwarding and flooding logic works by default.
		
		- 	STP is enabled by default.

The second bit of this chapter examines how switches work with these default settings,
showing how to verify the Ethernet learning and forwarding process.

Demonstrating MAC learning
****************************
	To see a switch's MAC address table, use the **show mac address-table** command.
	These command with no additional params, lists all known MAC addresses in the
	MAC table, including some overhead static MAC address that you can ignore.
	
	To see all dynamically learnt MAC addresses only, instead use the 
	**show mac address-table dynamic** command.
	
	Deleting all switch configuration:
	**erase startup-config** EXEC command to erase startup-config file.
	**delete vlan.dat** EXEC command to delete VLAN config details.
	**reload** EXEC command to reload the switch.
	**hotsname SW1** comand to set switch hostname.
	
	LAN switches forward Ethernet frames inside a VLAN. That means that if a frame 
	enters via a port in VLAN 1, then the switch will forward or flood that frame
	out other ports in VLAN 1 only; not out to any ports that happen to be assigned
	to another VLAN. (Chapter 11 Implementing Ethernet Virtual LANs).
	
Switch Interfaces
******************
	Check the status of those interfaces:
	**show interfaces status**
	
SW1# show interfaces status
	
Port Name Status Vlan Duplex Speed Type
Fa0/1 connected 1 a-full a-100 10/100BaseTX
Fa0/2 connected 1 a-full a-100 10/100BaseTX
Fa0/3 connected 1 a-full a-100 10/100BaseTX
Fa0/4 connected 1 a-full a-100 10/100BaseTX
Fa0/5 notconnect 1 auto auto 10/100BaseTX
Fa0/6 notconnect 1 auto auto 10/100BaseTX
Fa0/7 notconnect 1 auto auto 10/100BaseTX
Fa0/8 notconnect 1 auto auto 10/100BaseTX
Fa0/9 notconnect 1 auto auto 10/100BaseTX
Fa0/10 notconnect 1 auto auto 10/100BaseTX
Fa0/11 notconnect 1 auto auto 10/100BaseTX
Fa0/12 notconnect 1 auto auto 10/100BaseTX
Fa0/13 notconnect 1 auto auto 10/100BaseTX
Fa0/14 notconnect 1 auto auto 10/100BaseTX
Fa0/15 notconnect 1 auto auto 10/100BaseTX
Fa0/16 notconnect 1 auto auto 10/100BaseTX
Fa0/17 notconnect 1 auto auto 10/100BaseTX
Fa0/18 notconnect 1 auto auto 10/100BaseTX
Fa0/19 notconnect 1 auto auto 10/100BaseTX
Fa0/20 notconnect 1 auto auto 10/100BaseTX
Fa0/21 notconnect 1 auto auto 10/100BaseTX
Fa0/22 notconnect 1 auto auto 10/100BaseTX
Fa0/23 notconnect 1 auto auto 10/100BaseTX
Fa0/24 notconnect 1 auto auto 10/100BaseTX
Gi0/1 notconnect 1 auto auto 10/100/1000BaseTX
Gi0/2 notconnect 1 auto auto 10/100/1000BaseTX

SW1#


	The switch has 24 interfaces named FastEthernet and 2 named GigabitEthernet.
	
	NB::
		You can see the status for a single interface in a couple of ways; for
		instance, for F0/1 the command
			**show interfaces f0/1 status**
		lists the status in a single line of output.
		
	**show interfaces counters** lists stats abt incoming and outgoing frames on the
	interfaces; number of unicast, multicast and broadcast frames both in the in and
	out direction & total byte count for those frames.
	
SW1# show interfaces f0/1 counters

Port InOctets InUcastPkts InMcastPkts InBcastPkts
Fa0/1 1223303 10264           107       18

Port OutOctets OutUcastPkts OutMcastPkts OutBcastPkts
Fa0/1 3235055      13886       22940          437


Finding entries in the MAC address table
******************************************
	Viewing a known MAC address entry

SW1 # show mac address-table dynamic address 0200.1111.1111

Mac Address Table
-------------------------------------------
Vlan Mac Address Type Ports
---- ----------- -------- -----
1 0200.1111.1111 DYNAMIC Fa0/1
Total Mac Addresses for this criterion: 1

>>
	Sometimes you might be troubleshooting while looking at a network topology
	diagram and want to look at all the MAC address learnt off a particular port.
	IOS supplies that option with **show mac address-table dynamic interface**
	command.
	
	example

SW1 # show mac address-table dynamic fastEthernet 0/1

Mac Address Table
-------------------------------------------
Vlan Mac Address Type Ports
---- ----------- -------- -----
1 0200.1111.1111 DYNAMIC Fa0/1
Total Mac Addresses for this criterion: 1

>>
	Finally, you may want to find the MAC address in a single VLAN;- you can add the
	**vlan** param, followed by the VLAN number
	
	example
	
SW1 # show mac address-table dynamic vlan 1

Vlan Mac Address Type Ports
---- ----------- -------- -----
1 0200.1111.1111 DYNAMIC Fa0/1
1 0200.2222.2222 DYNAMIC Fa0/2
1 0200.3333.3333 DYNAMIC Fa0/3
1 0200.4444.4444 DYNAMIC Fa0/4
Total Mac Addresses for this criterion: 4

SW1 #
SW1 # show mac address-table dynamic vlan 2

Mac Address Table
-------------------------------------------
Vlan Mac Address Type Ports
---- ----------- -------- -----

SW1#

>>

Managing the MAC address table (Aging, Clearing)
*************************************************
	How the switch manages its MAC address table. Learnt MAC addresses do not stay
	there indefinitely. The switch will remove the entries due to age, due to table
	filling & you can remove entries using a command.
	
	For aging out MAC table entries, switches remove entries that not been used for 
	a defined number of seconds, (default of 300 seconds in many switches).
	
	To do this, switches look at every incoming frame, every source MAC address, and 
	does smth related to learning. If it is a new  MAC address, the switch adds the
	correct entry to the table of course. However, if that entry already exists, the
	switch still does smth: it resets the **inactivity timer** back to 0 for that
	entry.
	
	Each entry's timer counts upward over time to measure how long the entry has been 
	in the table. The switch times out (removes) any entry whose timer reaches the
	defined aging time.
	
	example
	
SW1 # show mac address-table aging-time

Global Aging Time: 300

Vlan Aging Time
---- ----------

SW1 #

SW1 # show mac address-table count

Mac Entries for Vlan 1:
---------------------------
Dynamic Address Count : 4
Static Address Count : 0
Total Mac Addresses : 4
Total Mac Address Space Available: 7299

SW1 #

>>
	If the table fills, a switch will remove the oldest entries, even if they are 
	younger than their aging time setting.
	
	The MAC address table uses content-addressable memory (CAM), a physical memory
	that has great table lookup capabilities.
	
	The size of the CAM depends on the particular model of the switch.
	
	Finally you can remove dynamic entries fromthe table MAC address table with the
	**clear mac address-table dynamic** command
	
	NB::
		show commands can be executed from user and enable mode, but the clear command
		happens to be a privilege mode command.
		

MAC Address Tables with Multiple Switches
*****************************************
	Example
	
Fred and Barney connected to SW1:
	Fred:
		PC1
		MAC address 0200.1111.1111
		F0/1
	Barney
		PC2
		MAC address 0200.2222.2222
		F0/2
		
out to SW2 through G0/1 and G0/2:
	Wilma
		PC3
		MAC address 0200.3333.3333
		F0/3
	Betty
		PC4
		MAC address 0200.4444.4444
		F0/4

>>
	For hosts connected to switch 1, if they communicated to host connected to switch2,
	switch's 1 mac address table would list its own port numbers (F0/1, F0/2 & G0/1).
	
	Similarly, switch'2 mac address table will list its own port numbers (F0/3, F0/4 &
	G0/2).
	
	example
	
SW1 # show mac address-table dynamic

Mac Address Table
-------------------------------------------
Vlan Mac Address Type Ports
---- ----------- -------- -----
1 0200.1111.1111 DYNAMIC Fa0/1
1 0200.2222.2222 DYNAMIC Fa0/2
1 0200.3333.3333 DYNAMIC Gi0/1
1 0200.4444.4444 DYNAMIC Gi0/1
Total Mac Addresses for this criterion: 4

! The next output is from switch SW2

SW2 # show mac address-table dynamic

1 0200.1111.1111 DYNAMIC Gi0/2
1 0200.2222.2222 DYNAMIC Gi0/2
1 0200.3333.3333 DYNAMIC Fa0/3
1 0200.4444.4444 DYNAMIC Fa0/4
Total Mac Addresses for this criterion: 4





