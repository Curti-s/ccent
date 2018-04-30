-09 Configuring Switch Interfaces
************************************
This chapter covers the following exam topics:
	2.0 LAN Switching Technologies
	2.3 Troubleshoot interface and cable issues (collisions, errors,duplex,speed)
	2.7 Configure, verify and troubleshoot port security
	2.7a Static
	2.7b Dynamic
	2.7c Sticky
	2.7d Max MAC address
	2.7e Violation actions
	2.7f Err-disable recovery
	
		
This chapter will show me how to configure and change the operation of switch
interfaces: how to change the speed, duplex or even disable the interface. That is the first half.

The second half will show me how to add security feature called port security, which monitor the source MAC address of incoming frames, deciding which frames are allowed and which cause security violations.

Do I Know This Already?
*************************

1.	Which of the following describe a way to disable IEEE standard **autonegation** on a **10/100** port on a cisco switch?
	 
	A. Configure the **negotiate disable** interface subcommand.
	B. Configure the **no negotiate** interface subcommand.
	C. Configure the **speed 100** interface subcommand.
	D. Configure the **duplex half** interface subcommand.
	E. Configure the **duplex full** interface subcommand.
	F. Configure the **speed 100** and **duplex full** interface subcommands.
	
	>> Configure the **speed 100** and **duplex full** interface subcommands.
		By default, the speed and duplex settings are set to auto. As a result,
		those interfaces attempt to automatically determine the speed and duplex
		settings to use.
		Switch to the interface mode and configure the speed and duplex.
	
2. In which of the following modes of the CLI could you configure the duplex setting for interface Fast Ethernet 0/5?
   
   A. User mode
   B. Enable mode
   C. Global configuration mode
   D. VLAN mode
   E. Interface configuration mode
   
   >> Interface configuration mode
		SW1# conf term
		SW1(config)# interface fa 0/5
		SW1(config-if)#
   
3. A Cisco Catalyst switch connects with its Gigabit0/1 port to an end user's PC. The end user thinking the user is helping, manually sets the PC's OS to use a speed of 1000Mbps and to use full duplex , and disables the use of autonegation. The switch's G0/1 port has default settings for speed and duplex. What speed and duplex settings will the switch decide to use (Choose 2 answers)

	A. Full duplex
	B. Half duplex
	C. 10 Mbps
	D. 1000 Mbps
	
	>> 1000Mbps and full duplex.
	
4.	Which of the following is required when configuring port security with sticky
	learning?
	
	A. Setting the maximum number of allowed MAC addresses on the interface with 
	   the **switchport port-security maximum** interface subcommand.
	B. Enabling port security with the **switchport port-security** interface 
	   subcommand.
	C. Defining the specific allowed MAC addresses using the **switchport port-security mac-address** interface subcomand
	D. All other answers list required commands.
	
	>> Enabling port security with the **switchport port-security** interface 
	   subcommand.
	
	
5. A switch's port Gi0/1 has been correctly enabled with port security. The 
   configuration sets the violation mode to restrict. A frame that violates the
   port security policy enters the interface, followed by a frame that does not.
   Which of the following answers correctly describe what happens in this 
   scenario? (choose 2 answers)
   
   A. The switch puts the interface into an err-disabled state when the first 
      frame arrives.
      
   B. The switch generates syslog messages about the violation of traffic for the
      first frame.
      
   C. The switch increments the violation counter for Gi0/1 by 1.
   
   D. The switch discards both the first and second frame.
   
   >> The switch generate syslog messages about the violation of traffic for the
   first frame.
   >> The switch increments the violation counter for Gi0/1

6. A cisco catalyst connects to what should be individual user PCs. Each port has
   the same port security config, configured as follows:
   
interface range gigabitethernet 0/1 - 24
switchport mode access
switchport port-security
switchport port-security mac-address sticky

	Which of the following answers describe the result of the port security 
	configuration created with these commands? (Choose 2 answers)
	
	A. Prevents unknown devices with unknown MAC address from sending data 
	through the switchports.
	
	B. If a user connects a switch to the cable, prevents multiple devices from
	sending data through the port
	
	C. Will allow any one device to connect to each port and will save that 
	device's MAC address into the startup-config
	
	D. Will allow any one device to connect to each port but will not save the
	device's MAC address into the startup-config.
	
	>>  Will allow any one device to connect to each port but will not save the
	device's MAC address into the startup-config.
	>> If a user connects a switch to the cable, prevents multiple devices from
	sending data through the port
	
	
	
	Answers
	1 F 2 E 3 A, D 4 B 5 B, C 6 B, D
	
	By the end I will have answers to this questions
	
	
Foundation Topics
---------------------
Configuring Switch Interfaces
*******************************

	IOS uses the term [interface] to refer to physical ports used to forward data
	to and from other devices. Configurations may differ among interfaces.
	
	IOS uses interface subcommands to configure these settings.
	
	The relatively basic per-interface settings: the port speed, duplex and a 
	text description. Also the most common pair interface subcommands: the
	**shutdown** and **no shutdown** commands which administrativel disable & 
	enable the interface respectively.
	
	This section ends with the topic on autonegation concepts, which dictate what
	settings a switch chooses to use when using autonegation.
	
Configuring Speed, Duplex and Description
*****************************************
	Example
	
Emma# configure terminal
Enter configuraion commands, one per line. End with CNTL/Z
Emma(config)# interface FastEthernet0/1
Emm(config-if)# duplex full
Emma(config-if)# speed 100
Emma(config-if)# description Printer on 3rd floor, Preset to 100/full is connected here.
Emma(config-if)# exit
Emma(config)# interface range FastEthernet 0/11 - 20
Emma(config-if-range)# description end users connect here.
Emma(config-if-range)# ^Z
Emma#



**show interfaces status** command lists much of the detail configured.
Example

Emma# show interfaces status
Port Name Status Vlan Duplex Speed Type
Fa0/1 Printer on 3rd floo notconnect 1 full 100 10/100BaseTX
Fa0/2 notconnect 1 auto auto 10/100BaseTX
Fa0/3 notconnect 1 auto auto 10/100BaseTX
Fa0/4 connected 1 a-full a-100 10/100BaseTX
Fa0/5 notconnect 1 auto auto 10/100BaseTX
Fa0/6 connected 1 a-full a-100 10/100BaseTX
Fa0/7 notconnect 1 auto auto 10/100BaseTX
Fa0/8 notconnect 1 auto auto 10/100BaseTX
Fa0/9 notconnect 1 auto auto 10/100BaseTX
Fa0/10 notconnect 1 auto auto 10/100BaseTX
Fa0/11 end-users connect notconnect 1 auto auto
10/100BaseTX
Fa0/12 end-users connect notconnect 1 auto auto
10/100BaseTX
Fa0/13 end-users connect notconnect 1 auto auto
10/100BaseTX
Fa0/14 end-users connect notconnect 1 auto auto
10/100BaseTX
Fa0/15 end-users connect notconnect 1 auto auto
10/100BaseTX
Fa0/16 end-users connect notconnect 1 auto auto
10/100BaseTX
Fa0/17 end-users connect notconnect 1 auto auto
10/100BaseTXFa0/18 end-users connect notconnect 1 auto auto
10/100BaseTX
Fa0/19 end-users connect notconnect 1 auto auto
10/100BaseTX
Fa0/20 end-users connect notconnect 1 auto auto
10/100BaseTX
Fa0/21 notconnect 1 auto auto 10/100BaseTX
Fa0/22 notconnect 1 auto auto 10/100BaseTX
Fa0/23 notconnect 1 auto auto 10/100BaseTX
Fa0/24 notconnect 1 auto auto 10/100BaseTX
Gi0/1 notconnect 1 auto auto 10/100/1000BaseTX
Gi0/2 notconnect 1 auto auto 10/100/1000BaseTX
	
	
	FastEthernet 0/1 (Fa0/1): This output lists a few characters of the 
	configured description. It also lists the configured speed of 100 and duplex
	full per the speed and duplex commands. However it also states that Fa0/1 has
	a status of notconnect, meaning that the interface is not currently working.
	
	FastEthernet 0/2 (Fa0/2): This port was not configured at all; has default
	config. Note the "auto" text under the speed and duplex, meaning this port 
	will attempt to autonegotiate both settings when the port comes up.
	
	FastEthernet 0/4 (Fa0/4): This port has default configs too, but it was 
	cabled to another working device & has completed the autonegotiation process.
	Therefore instead of "auto", the output lists the negotiatied speed and 
	duplex (a-full and a-100). 
	Note the text includes **a-** to mean that the listed speed and duplex values
	were negotiated.
	

Configuring multiple interface with interface range command
******************************************************************
**interface range FastEthernet 0/11 - 20** tells IOS that the next subcommands
apply interfaces Fa0/11 through Fa0/20.

Administratively Controlling Interface State with shutdown
***********************************************************
**shutdown**
**no shutdown**

	Example
	
SW1# configure terminal
Enter configuration commands, one per line. End with CNTL/Z
SW1(config)# interface fastEthernet0/1
SW1(config-if)# shutdown
SW1(config-if)#
*Mar 2 03:02:19.701: %LINK-5-CHANGED: Interface
FastEthernet0/1, changed state to administratively down
*Mar 2 03:02:20.708: %LINEPROTO-5-UPDOWN: Line
protocol on Interface FastEthernet0/1,
changed state to down
 
 
To bring the interface back up again, follow the same process but use **no shutdown**.

Two other important show commands: **show interface status** that lists one line
of input per interface, & when shutdowm, lists the interface status as "disabled"

**show interfaces** command without the status keyword, lists many lines of 
output per interface, giving much more detailed picture of interface status
and stats.

Example of the 2 show commands

SW1# show interfaces f0/1 status
Port Name Status Vlan Duplex Speed Type
Fa0/1 disabled 1 auto auto 10/100BaseTX


SW1# show interfaces f0/1
FastEthernet0/1 is administratively down, line
protocol is down (disabled)
Hardware is Fast Ethernet, address is1833.9d7b.0e81 (bia 1833.9d7b.0e81)
MTU 1500 bytes, BW 10000 Kbit/sec, DLY 1000
usec,
reliability 255/255, txload 1/255, rxload 1/255
Encapsulation ARPA, loopback not set
Keepalive set (10 sec)
Auto-duplex, Auto-speed, media type is
10/100BaseTX
input flow-control is off, output flow-control
is unsupported
ARP type: ARPA, ARP Timeout 04:00:00
Last input never, output 00:00:36, output hang
never
Last clearing of "show interface" counters never
Input queue: 0/75/0/0 (size/max/drops/flushes);
Total output drops: 0
Queueing strategy: fifo
Output queue: 0/40 (size/max)
5 minute input rate 0 bits/sec, 0 packets/sec
5 minute output rate 0 bits/sec, 0 packets/sec
164 packets input, 13267 bytes, 0 no buffer
Received 164 broadcasts (163 multicasts)
0 runts, 0 giants, 0 throttles
0 input errors, 0 CRC, 0 frame, 0 overrun, 0
ignored
0 watchdog, 163 multicast, 0 pause input
0 input packets with dribble condition detected
66700 packets output, 5012302 bytes, 0 underruns
0 output errors, 0 collisions, 1 interface
resets
0 unknown protocol drops
0 babbles, 0 late collision, 0 deferred
0 lost carrier, 0 no carrier, 0 pause output
0 output buffer failures, 0 output buffers
swapped out


Removing Configuration with the no command
********************************************

	With some IOS configurations, (but not all) you can revert to the default
	setting by issuing a **no** version of the command.
	
	For instance if you configured **speed 100** on interface, the **no speed**,
	on that same interface reverts to the default speed setting i.e
	(**speed auto**).
	
	Same idea with the **duplex** command: an earlier configuration of 
	**duplex half** or **duplex full**, followed by **no duplex** on the same
	interface, reverts back the config to duplex auto.
	
	For **no description** it reverts the interface to having no description.
	
	
Autonegotiation
****************
	For any 10/100/1000 or 10/100 interfaces; ie interfaces that run at diff
	speeds; Cisco catalyst switches default to a setting of **duplex auto** &
	**speed auto**.
	
	In prac, autonegotiation is easy; just leave the speed and duplex to default
	setting & let the switch port negotiate what settings to use on each port.
	However,problems occur due to unfortunate combinations of configs.
	
Autonegotiation Under working conditions
*******************************************
	
	Ethernet devices on the ends of a link must use the same standard or they 
	cannot correctly send data.
	For example, a NIC cannot use 100BASE-T, which uses 2-pair UTP cable with
	a 100Mbps speed, while the switch port on the other end of the link uses
	1000Base-T.
	
	Having both PC NICs and switchports that support multiple standards/speeds,
	makes it much easier to migrate to the next better standard.
	
	
	The IEEE autonegotiation protocol helps make it much easier to operate a
	LAN when NICs and switchports support multiple speeds.
	IEEE autonegotiation (IEEE standards 802.3u (100Mbps Base-T)), defines 
	protocol that lets the 2 UTP-based Ethernet nodes on a link to negotiate so
	that they each choose to use the same speed & duplex settings.
	
	Protocol messages, flow outside the normal Ethernet electrical frequencies,
	as out-of-band signal over the UTP cable. Basicaly each node states what it 
	can do & then each node picks the best option supporting both of them.
	
	Autonegotiation relies on the fact that the IEEE uses the same wiring pinouts
	for 10BASE-T and 100BASE-T and that 1000BASE-T simply adds to those pinouts,
	adding 2 pairs.
	
	Configuring both the speed and duplex on a cisco switch interface disbles 
	autonegotiation.
	
Port security
*************
	If the network engineer knows what device should be cabled and connected to
	a particular interface on a switch, the engineer can use **port security**
	to restrict that interface so that only expected devices an use it.
	
	Port security identifies devices based on the source MAC address of Ethernet
	frames which devices send.
	
	Port security has no restrictions on whether the frame cam from a local 
	device or it was forwarded through other switches.
	For instance, SW1 would use port security on its G0/1 interface, checking
	the source MAC address of the frame from PC2, when forwaded up to SW1
	from SW2.
	
	Port security has several flexible options, operating with the same core
	concepts. First switches enable port securit per port with diff settings
	available per port. Each port has a maximum number of allowed MAC addresses,
	meaning that for all frames entering that port, only a  number of diff
	source MAC addresses can be used in diff incoming frames before port
	security thinks a violation has occurred. When a frame with a new source MAC
	address arrives, pushing the number of MAC addresses past the allowed max,
	a port security violation occurs. At that point, the switch takes action - by
	default, discarding all future incoming frames on that port.
	
	Summary of ideas common to all variations of port security:
	
	- Define a max number of source MAC addresses allowed for all frames coming
	  in the interface.
	
	- Watch all incoming frames and keep a list of all source MAC addresses, plus
	a counter of the number of different source MAC addresses.
	
	- When adding a new source MAC address to the list, if the number of MAC
	addresses pushes past the configured max, a port security violation has
	occurred. The switch takes action; default action -> shutdown the interface.
	
	
	Predefining  MAC addresses for port security is optional.
	
	Port security provides an easy way to discover the MAC address used at each
	port using a feature called [sticky secure MAC addresses], where the learnt
	MAC address at the port is stored in a port security config(in the 
	running-config).
	
Configuring the port security
********************************

	First you need to disable the negotiation of a feature that isn't discussed
	until Chapter 11 Implementing Ethernet Virtual LANS, whether the port is an
	access or trunk port.
	
	Enable port security, set the max number of allowed MAC addresses per port
	& configure the actual MAC address as detailed in this checklist.
	
	>config checklist<
	
	Step 1.
	Make the switch interface either a static access or trunk interface using the
	**switchport mode access** or **switchport mode trunk** interface subcommand.
	
	Step 2.
	Enable port security using the **switchport port-security** interface 
	subcommand.
	
	Step 3.
	(Optional) Override the default max number of allowed MAC addresses 
	associated with the interface (1) by using the 
	**switchport port-security maximum number** interface subcommand.
	
	Step 4.
	(Optional) Override the default action to take upon a security violation
	(shutdown) using the 
	**switchport port-security violation {protect | restrict | shutdown}**
	interface subcommand.
	
	Step 5.
	(Optional) Predefine any allowed source MAC addresses for this interface,
	using the 
	**switchport port-security mac-address mac-address** command. Use it multiple
	times to define more than one MAC address.
	
	Step 6.
	(Optional) Tell the switch to "sticky learn" dynamically learned MAC 
	addresses with the
	**switchport port-security mac-address sticky** interface subcommand.
	
	NB:
	Port security does not save the config of the sticky addresses, so use the
	**copy running-config startup-config** command if desired.
	
	
	
Verifying port security
****************************

	Example
SW1# show running-config
(Lines omitted for brevity)
interface FastEthernet0/1
switchport mode access
switchport port-securityswitchport port-security mac-address
0200.1111.1111
!
interface FastEthernet0/2
switchport mode access
switchport port-security
switchport port-security mac-address sticky
!
interface FastEthernet0/3
switchport mode access
switchport port-security
!
interface FastEthernet0/4
switchport mode trunk
switchport port-security
switchport port-security maximum 8

	Based on the above running-config, i'll use the 
	**show port-security interface** command to list the config settings for
	port-securit on an interface.
	
SW1# show port-security interface fastEthernet 0/1
Port Security : Enabled
Port Status : Secure-shutdown
Violation Mode : Shutdown
Aging Time : 0 mins
Aging Type : Absolute
SecureStatic Address Aging : Disabled
Maximum MAC Addresses : 1
Total MAC Addresses : 0
Sticky MAC Addresses : 0
Last Source Address : Vlan : 0013.197b.500b:1
Security Violation Count : 1

SW1# show port-security interface fastEthernet 0/2
Port Security : Enabled
Port Status : Secure-up
Violation Mode : Shutdown
Aging Time : 0 mins
Aging Type : Absolute
SecureStatic Address Aging : Disabled
Maximum MAC Addresses : 1
Total MAC Addresses : 1
Configured MAC Addresses : 1
Sticky MAC Addresses : 1
Last Source Address:Vlan : 0200.2222.2222:1
Security Violation Count : 0

SW1# show running-config interface f0/2
Building configuration...
Current configuration : 188 bytes
!
interface FastEthernet0/2
switchport mode access
switchport port-security
switchport port-security mac-address sticky
switchport port-security mac-address sticky 0200.2222.2222
	

	Security violation has occured in FastEthernet 0/1 but none in
	FastEthernet0/2.
	
	The **show port-security interface fastEthernet 0/1** comman shows that the
	interface is in a [secure-shutdown] state, which means that the interface
	has been disabled because of port security.
	
Port Security Violation Actions
***********************************
	
	Finally, the switch can be configured to use one of 3 actions when violations
	occurr; which all cause the switch to discard the offending frame. But some
	of the options make the switch take additional actions.
	
	The actions include the sending of syslog messages to the console, sending
	SNMP trap messages to the network mgmt station & disabling the interface.
	
	Options of the 
	**switchport port-security violation {protect|resctrict|shutdown}** command:
	
	**switch port-security violation protect** ::
		- Discards offending traffic
		- Doesn't send log and SNMP messages
		- Doesn't increment the violation counter for each violating incoming
		frame.
		- Doesn't disable the interface by putting it in an err-disabled state,
		discarding all traffic.
		
	**switchport port-security violation restrict**
		- Discards offending frame.
		- Sends log and SNMP messages
		- Increments the violation counter for each violating incoming frame.
		- Doesn't disable the interface by putting it in err-disabled state, 
		discarding all traffic.
		
	**switchport port-security violation shutdown**
		- Discards the offending traffic
		- Sends log and SNMP messages
		- Increments the violation counter for each violating incoming frame.
		- Disables the interface by putting it in err-disabled state,discarding
		all traffic.
		
	NB:
	The shutdown option doesn't actually add the **shutdown** subcommand to the
	interface configuration. Instead, IOS puts the interface in an [err-disabled]
	state, which makes the switch stop all inbound and outbound frames.
	To recover from this state, someone must manually disable the interface
	**shutdown** interface command the enable the interface with the 
	**no shutdown** command.
	
Port Security MAC Address as Static and Secure but not dynamic
***************************************************************

	Once a switch port has been configure with port security, the switch no 
	longer considers MAC addresses associated with that port as being dynamic 
	entries as listed with the **show mac address-table dynamic** EXEC command.
	
	Even if the MAC addresses are dynamically learnt, once port security has
	been enabled, you need to use one of these options to see the MAC table 
	entries associated with using port security:
	 **show mac address-table secure** : List MAC addresses associated with ports
	 that use port security.
	 **show mac address-table static**: Lists MAC addresses associate with ports
	 that use port security, as well as any other statically defined MAC
	 addresses.

	




