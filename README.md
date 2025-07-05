<h1>Segmented VLAN-Based Branch Network with Inter-VLAN and WAN Routing (1/2)</h1>

<h2>Project Overview</h2>
This project was developed as part of a college-level networking curriculum to demonstrate applied knowledge of routing, switching, subnetting, VLANs, and WAN connectivity. It simulates a branch office environment that is integrated into a larger corporate or cloud-based infrastructure, using a combination of Layer 2 and Layer 3 devices.
The network design features three routers, three switches, internal servers, wireless connectivity, and an ISP simulation. It emphasizes secure and scalable communication between departments and external services through structured IP addressing and dynamic routing.

Key Features and Technologies:

-	Spoke-topology with RIPv2 routing protocol for dynamic route distribution across all routers.
-	Serial WAN links between routers using S1/0/x and S1/1/x interfaces with configured clock rates.
-	Variable Length Subnet Masking (VLSM) implemented using /30, /29, /28, and /25 subnets to optimize IP address allocation based on host requirements.
-	VLAN segmentation on switches:
    -	Switch 1 uses VLANs 10 and 20 for departmental segmentation.
    -	Switch 2 also uses VLANs 10 and 20; Switch 3 uses VLANs 30 and 40.
    -	VLAN assignments are based on port ranges to separate users (e.g., HR, IT, Admin).
-	Inter-VLAN routing performed through connected routers to enable cross-VLAN communication.
-	Trunking configured between switches to allow tagged VLAN traffic to traverse shared links.
-	DHCP configured on Routers 1 and 3 to dynamically assign IP addresses to PCs across different VLANs.
-	Static IP addressing applied to internal servers for reliable access to services such as file sharing and local applications.
-	Wireless access point deployed and connected to Router 1 to provide Wi-Fi connectivity for mobile devices.
-	End-to-end testing was performed using ping to verify full connectivity from local PCs and servers to the ISP server and external resources.

<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br />
<h2>Project walk-through:</h2>
Starting off the project, we are provided an internet connection that simulates an ISP. Server.com is the ISP server with an address of 11.1.1.10/24
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture2.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next, we will set up the physical layout of the network equipment. A network rack will hold three routers, three switches, two server, and a wireless router with a phone connected to the access point. while a nearby workstation table will include four computers for end-user access and testing. <br/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next we will add serial ports to all router before wiring the network <br/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next, we will begin wiring the network, starting with the routers. Serial cables will be used to connect the routers, with interface S1/0/1 designated as the clock rate interface for synchronous communication.
Router and Switch Connections:
•	Router 1 will connect to both Router 2 and Router 3 via serial interfaces. It will also connect to the ISP through G0/0/0, and to a wireless access point using G0/0/1.
•	Router 2 will connect to Router 1 and Router 3 via serial interfaces, and will be linked to Switch 1 through its Gigabit Ethernet port.
•	Router 3 will connect to Router 1 and Router 2 via serial interfaces, and will also be connected to Switch 2 via G0/0/0.
Switch Connections and VLAN Setup:
•	Switch 2 and Switch 3 will be connected using a trunk link to allow multiple VLANs to pass between them.
•	Switch 2 will be configured with:
o	VLAN 10 for ports F0/1–F0/11
o	VLAN 20 for ports F0/12–F0/24
•	Switch 3 will be configured with:
o	VLAN 30 for ports F0/1–F0/11
o	VLAN 40 for ports F0/12–F0/24
•	Each PC will be assigned to the appropriate VLAN based on its physical port and department.
•	Switch 1 will also be configured with VLANs 10 and 20, using a different subnet than Switch 2. It will connect to internal servers, each assigned to a separate VLAN.
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 <br />
<br />
Now it's time to configure the routers and bring all interfaces online. Each router’s serial interface (S1/0/1) will be configured with a clock rate of 500,000 to support synchronous communication on point-to-point WAN links.
To efficiently assign IP addresses across the network, we are implementing Variable Length Subnet Masking (VLSM). This allows us to allocate IP space based on the size and needs of each subnet:
•	/30 subnet: Used for point-to-point links for our routers, providing 4 total IPs and 2 usable addresses.
•	/29 subnet: Provides 8 total IPs and 6 usable addresses 
•	/28 subnet: Offers 16 total IPs with 14 usable addresses 
•	/25 subnet: Provides 128 total IPs and 126 usable addresses   <br/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 <br />
<br />
After bringing the router interfaces online, I proceeded to assign the appropriate IP addresses to each router interface. <br/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next, I configured the switches to support VLAN segmentation and trunking.
•	Switch 1 was divided into VLAN 10 and VLAN 20, with ports F0/1–F0/11 assigned to VLAN 10 and F0/12–F0/24 assigned to VLAN 20.
•	Switches 2 and 3 had their Gigabit ports configured as trunk ports to allow VLAN traffic to pass between switches.
•	Switch 2 was also configured with VLAN 10 and VLAN 20 using the same port ranges: F0/1–F0/11 for VLAN 10 and F0/12–F0/24 for VLAN 20.
•	Switch 3 was configured with VLAN 30 on ports F0/1–F0/11 and VLAN 40 on ports F0/12–F0/24.
  <br/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
I configured DHCP on Router 3 to automatically assign IP addresses to all connected computers within its network segment. Additionally, DHCP was set up on Router 1 to provide dynamic IP address allocation for devices on its side of the network. The DNS server used by all clients is located on the ISP server at IP address 11.1.1.10. After configuration, all computers successfully received IP addresses via DHCP.<br/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Static IP addresses were manually assigned to all servers to ensure consistent identification, stable connectivity, and reliable access to network services.
<br/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture10.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture11.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
RIPv2 was selected as the routing protocol for all routers to enable dynamic route exchange and maintain up-to-date routing tables across the entire network.     
<br/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture13.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture14.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture15.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 <br />
<br />
Next, we set up the wireless router by accessing its web-based GUI through a smartphone to complete the configuration.  
<br/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture19.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture20.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
A connectivity test was performed from the smartphone to the ISP server to verify that the wireless router was properly connected to the network and providing internet access. 
<br/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture19.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Lastly, we performed a connectivity test from all computers and servers to verify successful communication with the ISP server at IP address 11.1.1.10. We also confirmed internal network functionality by testing communication between the computers and the locally hosted server.  
<br/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture19.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture20.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
A connectivity test was performed to verify communication between the client devices and the internal servers.
<br/>
<img src="https://github.com/jessies98/Networking1.2/blob/main/images/Picture19.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
