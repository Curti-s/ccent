#Chapter 11 Implementing Ethernet Virtual LANs
**************************************
This chapter covers the following topics:
    
    2.0 LAN Switching Technologies
    2.1 Describe and verify switching concepts
    2.1a MAC learning and aging
    2.1b Frame switching
    2.1c Frame flooding
    2.1d MAC address table
    2.4 Configure, verify and troubleshoot VLANs (normal range) spanning multiple switches
    2.4a Access ports (data and voice)
    2.4b Default VLAN
    2.5a Trunk ports
    2.5b 802.1Q
    2.5c Native VLAN
    
    
Ethernet switches receive Ethernet frames, make decisions and then forward(switch) those Ethernet frames.
That core logic revolves around MAC addresses, the interface in which the frame arrives and the interfaces out
which the switch forwards the frame.

VLAN concept has the biggest impact on the choices made by a switch compared to other concepts.
This chapter examines the concepts of VLANs and their configuration.  The first major section
explains the core concepts which include;
    - how VLANs work on a single switch
    - how to use VLAN trunking to create VLANs that span across multiple switches
    - how to forward traffic btwn VLANs using a router.

The second major section shows how to configure VLANs and VLAN trunks: how to statically assign interfaces
into a VLAN.

#Do I Know This Already?
*********************

1. In a LAN, which of the following terms best equates to the term VLAN?
    
    a. Collision domain
    b. Broadcast domain
    c. Subnet
    d. Single switch
    e. Trunk
    
    >> Broadcast domain
    
2. Imagine a switch with 3 configured VLANs. How many IP subnets are required, assuming that all hosts
in all VLANs want to use TCP/IP?
    
    a. 0
    b. 1
    c.  2
    d. 3
    
    >> 3
    
    
3. Switch SW1 sends a frame to Switch SW2 using 802.1Q trunking. Which of the answers describes how 
SW1 changes or adds to the Ethernet frame before forwarding the frame to SW2?

    a. Inserts a 4-byte header and does change the MAC addresses
    b. Inserts a 4-byte header and does not change the MAC addresses
    c. Encapsulates the original frame behind an entirely new Ethernet header'
    d. None of the above
    
4. Imagine you are told that switch 1 is configured with dynamic auto parameter for trunking on its
Fa0/5 interface, which is connected to switch2. You have to configure switch2. Which of the following settings
for trunking could allow trunking to work? (Choose 2 answers)

    a. on
    b. dynamic auto
    c. dynamic desirable
    d. acces
    e. none 
    
5. A switch has just arrived from Cisco. The switch has never been configured with any VLANs, but VTP
has been disabled. An engineer gets into configuration mode and issuse the vlan 22 command, followed by the
name **Hannahs-VLAN** command. Which of the following are true? (Choose 2 answers)

    a. VLAN 22 is listed in the output of the show vlan brief command
    b. VLAN 22 is listed in the output of the show running-config command
    c. VLAN 22 does not exist in that switch until at least one interface is assigned to that VLAN.
    d . VLAN 22 is not created by this process.
    
6. Which of the following commands identify switch interfaces as being trunking interfaces: interfaces that
currently operate as VLAN trunks? (Choose 2 answers)

    a. show interfaces
    b. show interfaces switchport
    c. show interfaces trunk
    d. show trunks
    
  Answers
  1 B 2 D 3 B 4 A, C 5 A, B 6 B, C
    
    
##Foundation Topics
###VLAN Concepts

LAN -> all devices in the same broadcast domain.
Without a VLAN, a switch considers all its interface to be in the same broadcast domain ie. when a broadcast
frame enters one switch port, the switch forwards the frame out to all other ports.
With VLAN support, a switch can create multiple broadcast domains called **Virtual LANs**.

Some of the reasons for separating hosts into VLANs include;
    - reducing the number of hosts that waste effort processing unneeded broadcasts. / reducing CPU
    overhead on each device.
    - reducing security risks, because fewer hosts see frames sent by any one host.
    - improve security for hosts that send sensitive data by keeping those hosts on a separate VLAN.
    - solve problems more quickly because the failure domain for many problems is the same set of devices
    as those in the same broadcast domain
    - **reduce the workload for the spanning tree protocol by limiting VLAN into a single access switch**.
    
### Creating multiswitch VLANs using trunking
*************************************

Configuring VLANs on a single switch requires little or no effort: simply configure each port to tell it the
VLAN number to which the port belongs.  With multiple switches, you have to consider additional concepts
abt how to forward traffic between the switches.

Switches need to use ** VLAN trunking** on the links btwn switches. VLAN trunking causes the switch to
use a process called **VLAN tagging**, by which the sending switch addds another header to the frame before
sending it over the trunk. 
This extra trunking header includes a **VLAN identifier** (VLAN ID) field so that the sending switch can 
associate the frame with a particular VLAN ID and receiving switch can then know in what VLAN each frame 
belongs.        

###VLAN Tagging Concepts
**********************

VLAN trunking creates 1 link btwn switches that supports as many VLANs as you need.
A switch treats a VLAN trunk link as if it were part of all the VLANs.
At the same time, the trunk keeps the VLAN traffic separate. Frames in VLAN10 would not got to
devices in VLAN20, because each frame is identifie by VLAN number as it crosses th trunk.

Trunking allows switches to pass frames from multiple VLANs over a single physical connection by adding
a small header to the Ethernet frame.


## 802.1Q and ISL VLAN Trunking protocols
**********************************

Cisco has supported 2 diff trunking protocols over the years:
    - Inter-Switch Link and
    - IEEE 802.1Q
    
IEEE 802.1Q is the most popular trunking protocol; it defines a dif way to do trunking.
While both ISL and 802.1Q tag each frame with the VLAN ID, the details differ. 802.1Q inserts an extra
4-byte 802.1Q VLAN header into the original frame's Ethernet header. As for the fields in the 802.1Q header,
only 12-bit VLANID field inside the header matters.
The 12-bit field supports a theoretical maximum of 21^12 (4096) VLANS, but in practice it supports a max
of 4094. 
NB::
        Both 802.1Q and ISL use 12 bits to tag the VLAN ID, with 2 reserved values [0 and 4095].

802.1Q header comprises of the following;
    Type
    Priority
    Flag
    VLAN ID (12bit)
    
Cisco switches break the range of VLAN IDs (1-4094) into 2 ranges;
    - normal range
    - extended range
    
All switches can use the normal-range VLANs with values from 1- 1005
Only some switches use extended range VLANS with VLAN IDs frome 1006 to 4094. The rules for which 
switches can use extended-range VLANs depend on the connfiguration of the **VLAN Trunking Protocol**
(VTP).

802.1Q also defines one special VLAN ID on each trunk as the **native VLAN** (defaulting to use VLAN1).
By definition, 802.1Q does not add an 802.1Q header to frames inside the native VLAN. When a switcch on 
the other side of the trunk receives a frame that doesn't have an 802.1Q header, the receiving switch knows
that the frame is part of the native VLAN.
NB::
        Because of this behavior, both switches must agree on which VLAN is the native VLAN.
        
802.1Q provides some interesting functions, mainly to support connections to devices that do not undertand
trunking. For instance, when cabling a to a switch that doesn't understand 802.1Q trunking, a Cisco switch 
could send frames in the native VLAN- meaning that the frame has no trunking header- so the other switch 
could understand the frame.

The native VLAN concept give switches the capability of at least passing traffic in one VLAN(native VLAN)
which can allow some basic functions, like reachability to telnet into a switch.


### Forwarding Data btwn VLANs
****************************
#### Routing packets btwn VLANs with a router
**************************************
The job of forwarding data into and out of a VLAN falls to routers. Instead of switching layer 2 Ethernet 
frames btwn 2 VLANs, the network must route layer3 packets btwn 2 subnets.

** Router on a stick**

This chapter introduces the core concepts of routing IP packets btwn VLANS, or more accurately, btwn
subnets on VLANs. Chapter 18, Configuring IPv4 Addresses an Static routes, shows how to configure 
designs that use an external router with router-on-a-stick.

### VLAN and VLAN Trunking Configuration and Verification
***********************************************
VLANs are broadcast domains created through a configuration.
This section separates the VLAN configuration details into 2 major sections. The first section looks at how
to configure access interfaces, which are switch interfaes that do not use VLAN trunking.
The second part shows how to configure interfaces that do use VLAN trunking.

### Creating VLANs and assigning access VLANs to an Interface.
*************************************************
- Create a VLAN.
- Give the VLAN a name
- Assign interfaces into a VLAN.
(VLAN trunking not required here)

For a cisco switch to forward frames in a particular VLAN, the switch must be configured to believe that the
VLAN exists. In addition, the switch must have non-trunking interfaces called **access interfaces**, assigned
to the VLAN , and /or trunks that support the VLAN.

Configuration steps for access interface are as follows;

    Step1: To configure new VLAN, follow these steps;
        
        A. From config mode, use the vlan vlan-id command in global config mode to create the VLAN
        and move the user into VLAN configuration mode.
        
        B. (Optional) Use the **name** name command in the VLAN configuration mode to list a name
        for the VLAN. If not configured, the VLAN name is VLANZZZZ, where ZZZZ is the 4-digit decimal
        VLAN ID.
    
    Step2. For each access interface (each interface that does not trunk, but instead belongs to a single
    VLAN), follow these steps:
        
        A. Use the interface type number command in global configuration mode to move into interface config
        mode for each desired interface.
        
        B. Use the switchport access vlan id-number command in interface config mode to specify the VLAN
        number associated with that interface.
        
        C. (Optional) Use the switchport mode access command in interface configuration mode to make this
        port always operate in access mode (that is not trunk)
        

Example

SW1# configure terminal
Enter configuration commands, one per line. End with CNTL/Z
SW1(config) # vlan 2
SW1(config-vlan)# name Freds-vlan
SW1(config-vlan)# exit
SW1(config) # interface range fastethernet 0/13 -14
SW1(config-if) # switchport access vlan 2
SW1(config-if) # switchport mode access
SW1(config-if) # end
 
 ! Below, the show running-config command lists the interfaces subcommands on  interfaces
 ! Fa0/13 and Fa0/14
 
SW1# show running-config
! Many lines omitted for brevity
! Early in the output:
vlan 2
name Freds-vlan

!
! more lines omitted for brevity
interface FastEthernet0/13
switchport access vlan 2
switchport mode access
!
interface FastEthernet0/14
switchport access vlan 2
switchport mode access
!


SW1# show vlan id 2
VLAN Name Status Ports
---- -------------------------------- ---------
-------------------------------
2 Freds-vlan active Fa0/13, Fa0/14



### VLAN trunking protocol
***********************
A proprietary tool in Cisco switches that advertise each VLAN configured in one switch., with the vlan number
command, so that all other switches in the campus learn about that VLAN.
However, for various reasons,many enterprises choose not to use VTP.
























    
