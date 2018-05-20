Recap:
	Part 1 provided a broad look at the fundamentals of all parts of networking.
	Part 2 and 3 now drill into depth about details of Ethernet.
	
Goals:
	Chapter 6 will help me see how to get into the CLI of a switch
	
	Chapter 7 takes a close look at Ethernet switching; ie the logic
	used by a switch.
	
	Chapter 8 shows the ways to configure a switch for remote access 
	with Telnet and Secure Shell (SSH) along with a variety of other
	useful commands that will help you when you work with any real 
	lab gear, simulator etc.
	
	Chapter 9, the final shows how to configure switch interface for
	several important features: port security and inter-related features
	of speed, duplex and autonegotiation.
	

- 06 Using the Command Line Interface
****************************************
	Covers the following topics:
		1.0 Network Fundamentals
		1.6 Select appropriate cabling type based on implementation
			requirements.
			
		This chapter primarily explains foundational skills required 
		before you can explore the roughly 20exam topics that use the
		verbs **configure** , **verify** and **troubleshoot**.
		

Do I Know This Already?
************************

1.	In what modes can you type the command show mac address-table
	& expect to get a response with MAC table entries? (Choose 2 
	answers).
	  
	  A. User mode
	  B. Enable mode
	  C. Global configuration mode
	  D. Interface configuration mode
	  
	  >> User mode and Enable mode
	  
2.	In which of the following modes of the CLI could you type the 
	command **reload** and expect the switch to reboot?
	
	 
	  A. User mode
	  B. Enable mode
	  C. Global configuration mode
	  D. Interface configuration mode
	  
	  >> Enable mode
	  
3.	Which of the following is a difference between Telnet and SSH as 
	supported by a Cisco switch?
	
	 A. SSH encrypts the passwords used at login, but not other traffic;
	 	Telnet encrypts nothing.
	 B.	SSH encrypts all data exchange, including login passwords;
	 	Telnet encrypts nothing
	 C.	Telnet is used from Microsoft OS and SSH is used from UNIX and
	 	Linux OS.
	 D. Telnet encrypts only password exchanges; SSH encrypts all data
	 	exchanges.
	 	
	 >> SSH encrypts all data exchange, including login passwords;
	 	Telnet encrypts nothing.
	 	
4.	What type of switch memory is used to store the configuration used 
	by the switch when it is up and running?
	
	 A.	RAM
	 B. ROM
	 C. Flash
	 D. NVRAM
	 E. Bubble
	 
	 >> RAM
	 
5.	What command copies the configuration from RAM into NVRAM?
	
	 A. copy running-config tftp
	 B. copy tftp running-config
	 C. copy runnig-config startup-config
	 D. copy startup-config running-config
	 
	 >> copy running-config startup-config
	 
6.	A switch user is currently in console line configuration mode. 
	Which of the following would place the user in enable mode?
	(Choose 2 answers)
	
	 A. Using exit command once
	 B. Using the end command once
	 C. Pressing the Ctrl+Z command once
	 D. Using quit command
	 
	 >> Using the exit command once & Pressing Ctrl+Z command once.
	 

Accessing the Cisco catalyst switch CLI
***************************************

	Cisco produces a wide variety of switch series or familes, each series
	comprising of specific models of switches that have similar feature,
	similar price-versus performance trade-offs and similar components.
	
	For instance Cisco 2960-X series of switches; fully featured, low cost
	wiring closet switches for enterprises.
	
	Cisco refers to a switch's physical connector as either interface or
	ports, with an interface type and interface number. Interface type is 
	used in commands on the switch; ie Ethernet, Fast Ethernet, Gigabit
	Ethernet and so on for faster speeds.
	
	Ethernet interface supporting multiple speeds: the permanent name for the
	interface refers to the fastest supported speed. For instance 10/100/1000 
	interface( an interface running at 10Mbps, 100Mbps and 1000Mbps) would be 
	called Gigabit Ethernet no matter what speed is currently in use.
	
	Uniquely numbering of interfaces, some catalyst switches use 2-digit interface
	number (x/y),while others use 3-digit number (x/y/z). For instance, 2  
	10/100/1000 ports on many older Cisco catalyst switches would be called
	Gigabit Ethernet 0/0 and Gigabit Ethernet 0/1, while on newer 2960-X 
	series, 2 interfaces would be Gigabit Ethernet 1/0/1 and Gigabit Ethernet
	1/0/2.
	

IOS CLI
*******
	Cisco OS is called Internetwork Operating System (IOS).
	
	The Cisco IOS CLI can be accessed in 3 possible ways:
		* the console
		* Telnet
		* SSH
		
	Telnet and SSH use IP network in which the Switch resides in.
	Console access requires both a physical connection between a 
	PC and switch's console port, as well as some software on the
	PC.
	
Cabling the Console connection
*******************************
	
	After the PC physically connects to the console port, a terminal
	emulator software package must be installed and configured in the 
	PC. The terminal emulator must be configured to use the PC's 
	serial port to match the settings on the switch's console port.
	
	Default console port settings on a switch are as follows:
		- 9600 bits/second
		- No hardware flow control
		- 8-bit ACSII
		- No parity bits
		- 1 stop bit
		
		NB:
			The last 3 params are referred to collectively as 8N1.

Accessing the CLI with Telnet and SSH
*****************************************

	Telnet uses the concept of a Telnet client (terminal application)
	and a Telnet Server(switch).
	Caveat for telnet is that it sends all data including username and
	password for login to the switch as clear text data. (port 23)
	
	SSH is a much more secure option compared to Telnet. It encrypts all
	messages, including passwords , avoiding the possiblity of someone 
	capturing packets in the network. (port 22)
	
User and Enable (Privilege) Modes
*********************************
	User mode / User Exec mode, allows the user to look around but not
	break anything
	
	Enable mode / Privilege mode, powerful/privilege commands can be executed
	here.
	
	NB::
		If the command prompt lists the hostname followed by a >,
		the user is in user mode; it is hostname followed by the #,
		the user is in enable mode.
		

Password Security for CLI Access from the Console
**************************************************
	A Cisco switch with default settings, remains relaively secure when
	locked inside a wiring closet, because by default, a switch allows 
	console access only.
	
	By default,the console requires no password at all and no password
	to reach enable mode for users that happened to connect from the 
	console.
	
	Simple passwords can be configured at 2 points in the login process
	from the console: when the user connects from the console and when
	any user moves to enable mode(using the **enable** EXEC) command.
	
	Example
	
Certskills1#  **show running-config**
! Output has been formated toshow only the parts relevant to this discusion
hostname Certskills1
!
enable secret love
!
line console 0
login
password faith
! The rest of the output has been mitted
Certskills1#


	Working from top to bottom, note the first config command 
	**show running-config** and next note the lines with a **!**
	in them; they are comment lines both in the text and real 
	switch.
	
	The **enable secret love** config command defines the password
	that all users must use to reach enable mode; no matter if the user
	uses console, telnet or ssh.
	
	Finally **line console 0**, is the command that identifies the console,
	meaning that the next commands apply to the console only.
	
	The **login** command tells the IOS to perform simple password checking
	at the console. By default the switch doesn't ask for a password for 
	console users.
	
	Finally, the **password faith** command defines the password the console
	user must type when prompted. 

Debug and show commands
****************************
	Single most popular Cisco IOS command is the **show** command. 
	Essentially, it lists the currently known facts about the
	switch operation status.
	
	For instance, **show mac adddress-table dynamic** command,
	issued from **user mode**, lists the table that the switch
	uses to make forwarding decisions.
	
	The **debug** command also tells the user details about the 
	operation of the switch. However, while the **show** command
	lists status information at one instant of time- more like 
	a photograph, the **debug** command acts more like a video 
	camera feed. Once you issue the command. IOS remembers, 
	issuing messages that an switch user can choose to see. The console
	sees these messages by default.
	
	
Configuring Cisco IOS software
*********************************
	Configuration mode, contains a multitude of commands. To help
	organize the configuration, IOS groups some kind of configuration
	commands together. To do that when using configuration mode, you
	move from the initial mode-global configuration mode- into 
	subcommand modes using **context-setting commands**; they move you 
	from one configuration subcommand mode, or context to another.
	
	The context-setting commands tell the switch about which topic you 
	will enter the next few config commands. More importantly, they tell
	the switch the topic you care about right now, so when you use the **?**
	to get help, the switch gives you help about that topic only.
	
	For instance **interface** command, one of the commonly used
	context-setting configuration commands.
	eg
		**interface FastEthernet 0/1**
	Asking for help in interface configuration mode displays only 
	commands that are useful when configuring Ethernet interfaces.
	
	Commands used in this context are called **sub commands** or
	in this specific case **interface subcommands**.
	
	
	Example
	
	The following are a series of steps in a cisco switch:
	
	- Movement from enable mode to global configuration mode using the
	  **configure terminal** EXEC command
	  
	- Using **hostname Fred** global config command to configure the switch's
	  name.
	  
	- Movement from global config mode to console line config mode using the
	  **line console 0** command
	  
	- Setting the console's simple password to **hope** using the 
	  **password hope** line subcommand.
	  
	- Setting the speed to 100Mbps for interface Fa0/1(using the **speed 100**)
	  interface command.
	  
	- Movement from interface config mode back to global config mode using the
	  **exit** command.
	  
	  
Switch# **configure terminal**
Switch(config)# **hostname Fred**
Fred(config)#**line console 0**
Fred(config-line)# **password hope**
Fred(config-line)# **interface FastEthernet 0/1**
Fred(config-if)#**speed 100**
Fred(config-if)# **exit**
Fred(config)#


Example of some common modes used for global configuration mode:
	
	**hostname(config)#** -> Global config mode / None(first mode after conf terminal)
	
	**hostname(config-line)#** -> Line config mode --- line console 0 / line vty 0 15
	
	**hostname(config-if)#** -> Interface config mode --- interface [type number]
	
	**hostname(vlan)#** VLAN config mode ---------- vlan [number]
	
	
Storing Switch Configuration Files
************************************
	When configuring a switch, it needs to use the config, also 
	needs to be able to retain the config in case the switch loses
	power.
	
	Cisco switches contain RAM to store data while the Cisco IOS
	is using it, but RAM is volatile.
	
	To store information that must be retained when the switch loses
	power or is reloaded, Cisco switches use several types of more 
	permanent memory, none of which has any moving parts.
	
	By avoiding moving parts, switches can maintain better uptime
	and availability.
	
	Types of memory found in Cisco switches:
		RAM:
			Also DRAM, for dynamic random access memory.
			The running (active) configuration file is
			stored here.
			
		Flash memory:
			Either a chip inside the switch or a removable
			memory card; it stores fully functioning Cisco
			IOS images and it's the default location where
			switch gets it Cisco IOS at boot time.
			It can also be used to store other files,
			including backup copies of configurations files.
			
		ROM:
			Read Only memory stores a bootstrap(or boothelper)
			program that is loaded when the switch first powers
			on.
			This bootstrap program, then finds the full Cisco
			IOS image and manages the process of loading
			Cisco IOS into RAM, at which point Cisco IOS takes'over 
			operation of the switch.
			
		NVRAM:
			Non-Volatile RAM, stores the initial startup configuration
			file that is used when the switch is first powered on
			and when the switch is reloaded.
			
	Cisco IOS stores the collection of configuration commands in the
	**configuration file**. 
	Switches use multiple config files- one for the initial config used 
	when powering on and another config for the active, currently
	used running configuration as stored in RAM.
	
Erasing configuration files
	Done using 3 different commands:
		**write erase**
		**erase startup-config**
		**erase nvram:**
		
	Note that the Cisco IOS does not have a command that reases the contents 
	of the running-config file., therefore, inorder to clear out the
	running-config fie, simply erase the startup-config & reload the switch &
	the running -config will be empty at the end of the process.
		
