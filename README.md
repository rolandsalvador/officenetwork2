<h1>Small Office Network (Part 2) - Configuration</h1>

<h2>Description</h2>
In this project, I created a small office network from scratch in Cisco Packet Tracer. This repository is the first part of two in my small office network project. <a href="https://github.com/rolandsalvador/officenetwork">Part 1</a> is creating the network from scratch, and part 2 is configuring the network to use the many protocols and services required in an office. 
<br />
<br />
I wanted to put my networking knowledge to the test after obtaining my Cisco Certified Network Associate (CCNA) certification. Though the CCNA exam had practical questions that required me to apply what I learned, I wanted to take it one step further by designing a network from the ground up and configure it as if it were a real small office network. Thank you for taking a look, and please make sure to check out <a href="https://github.com/rolandsalvador/officenetwork">part 1</a> if you haven't yet!
<br />
<br />
The network is a two-tier, or collapsed core, design with a PC, laptop, phone, server, wireless LAN controller, and lightweight access point. The full topology can be seen below.
<br />
<br />
<img src="https://i.imgur.com/qUnA3Qz.png"/>

<h2>Skills Used</h2>

- <b>Network Administration</b>
- <b>Network Protocols</b>
- <b>OSI Model</b>
- <b>Subnets</b>
- <b>VLANs</b>
- <b>Firewalls/ACLs</b>
- <b>IP Addressing</b>

<h2>Environments Used</h2>

- <b>Cisco Packet Tracer</b>

<h2>Contents</h2>

[1. Hostnames](#1-hostnames)<br />
[2. EtherChannel](#2-etherchannel)<br />
[3. Trunk ports and Dynamic Trunking Protocol (DTP)](#3-trunk-ports-and-dynamic-trunking-protocol-dtp)<br />
[4. VLAN Trunking Protocol (VTP)](#4-vlan-trunking-protocol-vtp)<br />
[5. Virtual Local Area Networks (VLANs)](#5-virtual-local-area-networks-vlans)<br />
[6. Access ports](#6-access-ports)<br />
[7. Disabling unused ports](#7-disabling-unused-ports)<br />
[8. IPv4](#8-ipv4)<br />
[9. Hot Standby Router Protocol (HSRP)](#9-hot-standby-router-protocol-hsrp)<br />
[10. Spanning Tree Protocol (STP)](#10-spanning-tree-protocol-stp)<br />
[11. Open Shortest Path First (OSPF) and IPv4 Routes](#11-open-shortest-path-first-ospf-and-ipv4-routes)<br />
[12. Dynamic Host Configuration Protocol (DHCP)](#12-dynamic-host-configuration-protocol-dhcp)<br />
[13. Domain Name System (DNS)](#13-domain-name-system-dns)<br />
[14. Network Time Protocol (NTP)](#14-network-time-protocol-ntp)<br />
[15. Simple Network Management Protocol (SNMP)](#15-simple-network-management-protocol-snmp)<br />
[16. Syslog](#16-syslog)<br />
[17. File Transfer Protocol (FTP)](#17-file-transfer-protocol-ftp)<br />
[18. Secure Shell (SSH) and Access Control Lists (ACLs)](#18-secure-shell-ssh-and-access-control-lists-acls)<br />
[19. Network Address Translation (NAT)](#19-network-address-translation-nat)<br />
[20. Link Layer Discovery Protocol (LLDP)](#20-link-layer-discovery-protocol-lldp)<br />
[21. Port Security](#21-port-security)<br />
[22. DHCP Snooping](#22-dhcp-snooping)<br />
[23. Dynamic ARP Inspection (DAI)](#23-dynamic-arp-inspection-dai)<br />
[24. IPv6](#24-ipv6)<br />
[25. Wireless Networking](#25-wireless-networking)<br />
[26. Security](#26-security)<br />
[Conclusion](#conclusion)

<h2>Walkthrough</h2>

Before we start, I want to clarify that there may be screenshots from only one device’s configurations when I say that it is for multiple. In these cases, it means that the set of commands are the same across multiple devices. I did not screenshot their configurations because it would be redundant.

<h3>1. Hostnames</h3>
The first thing I did was configure each device’s hostname so that I could differentiate which CLI I’m working with.
<br />
<br />
<img src="https://i.imgur.com/Ge5T4b9.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>2. EtherChannel</h3>
EtherChannel combines multiple physical links into a single logical link, providing redundancy, load balancing, and increased bandwidth. Interfaces G1/0/1 and G1/0/2 between DSW1 and 2 will be bundled together into Port-channel1.
<br />
<br />
<img src="https://i.imgur.com/2Wo4GgE.png"/>
Using “do show etherchannel summary” we can see that Po1 has been successfully created.
<br />
<br />
<img src="https://i.imgur.com/SdEwSmQ.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>3. Trunk ports and Dynamic Trunking Protocol (DTP)</h3>
Trunk ports allow traffic from multiple VLANs to pass through an interface. This is essential for logically separating traffic seamlessly and securely. Using “do show cdp neighbors” we can see the local switch interfaces connected to its neighbors.
<br />
<br />
<img src="https://i.imgur.com/yImRKoN.png"/>
Interfaces G1/0/4 to G1/0/6 on DSW1 and 2 are connected to ASW1, 2, and 3. I configure the trunk links on these interfaces because the traffic between the endpoints and distribution switches will all flow through here.
<br />
<br />
<img src="https://i.imgur.com/e2t6XFq.png"/>
I also disabled Dynamic Trunking Protocol (DTP) because I want these ports to stay as trunk links. As a security best practice, I disabled DTP since it’s not in use. Additionally, I changed the native VLAN to an unused VLAN as another security best practice.
<br />
<br />
<img src="https://i.imgur.com/CtOYsPj.png"/>
I performed the same configurations on ASW1, 2, and 3’s F0/1 and F0/4 interfaces, which are connected to both DSW1 and 2.
<br />
<br />
<img src="https://i.imgur.com/WcRcWtV.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>4. VLAN Trunking Protocol (VTP)</h3>
VTP lets us propagate and sync VLAN configurations across multiple switches in the same domain. This saves a lot of manual configuration, since the VLAN configurations on the client switches will automatically sync to the server switches configurations.
<br />
<br />
<img src="https://i.imgur.com/BJkJKgk.png"/>
On the VTP server (DSW1), I changed the domain name to grilledonion and set VTP to version 2.
<br />
<br />
<img src="https://i.imgur.com/IydGQCL.png"/>
On the VTP clients (ASW1, 2, 3), I set the VTP mode to client, and the configurations on DSW1 were automatically applied. Note that DSW2 is also a server, but it also synced to DSW1’s changes.
<br />
<br />
<img src="https://i.imgur.com/X0Xv5Uo.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>5. Virtual Local Area Networks (VLANs)</h3>
Now that VTP is set up, I set up the VLANs that I’ll be using for this project. VLAN 10 for PCs, VLAN 20 for phones, VLAN 30 for servers, VLAN 40 for Wi-Fi, and VLAN 99 for management.
<br />
<br />
<img src="https://i.imgur.com/obKl1r7.png"/>
The same commands were used on the access switches.
<br />
<br />
<img src="https://i.imgur.com/R01U7Z7.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>6. Access ports</h3>
Access ports only allow traffic from one VLAN, and these are for endpoints. For security reasons, we want each endpoint to send traffic in one VLAN only, which is why I have separate VLANs for each endpoint.
<br />
<br />
On ASW1, F0/2 is connected to LWAP1, which is not using FlexConnect. LWAP1 will relay all the traffic from wireless endpoints through management VLAN 99, so I configured F0/2 as an access port on VLAN 99.
<br />
<br />
<img src="https://i.imgur.com/Rvud2tf.png"/>
On ASW2, I configured F0/2 with similar settings, but with VLAN 10 for PCs and VLAN 20 for phones.
<br />
<br />
<img src="https://i.imgur.com/yQsf8Gp.png"/>
Again, on ASW3 I used similar settings but with VLAN 30 for the server.
<br />
<br />
<img src="https://i.imgur.com/V9FMFQX.png"/>
Back on ASW1, I explicitly configured F0/3, the interface connected to WLC1, as a trunk port. WLC1 must support management VLAN 99 and Wi-Fi VLAN 40, so it cannot be an access port.
<br />
<br />
<img src="https://i.imgur.com/riob2RF.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>7. Disabling unused ports</h3>
As a security best practice, I disabled all unused ports on all switches. “do show interfaces status” displays all the unused ports.
<br />
<br />
<img src="https://i.imgur.com/IFBYVDy.png"/>
For example, DSW1’s interfaces G1/0/7 through 24 and G1/1/1 through 4 interfaces are unused, so I shut them down.
<br />
<br />
<img src="https://i.imgur.com/4FjGyUH.png"/>
In addition, I used the “do write” command after every step in this project to ensure that my changes are saved.
<br />
<br />
<img src="https://i.imgur.com/lO70pwO.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>8. IPv4</h3>
The internal network address that I used in this project is the 192.168.0.0/24 network, and the 203.0.113.0/24 network acts as the outside network.
<br />
<br />
<img src="https://i.imgur.com/MaZG5e7.png"/>
The network addresses for the other devices are listed below.
<br />
<br />
<img src="https://i.imgur.com/IlYKdvC.png"/>
On R1, interface G0/0 and G0/1 face DSW1 and 2 and are assigned their respective point-to-point addresses. G0/2 faces the Internet and is assigned by the ISP through DHCP. In addition, I added Loopback1 for use in future configurations. 
<br />
<br />
<img src="https://i.imgur.com/Srvo2nb.png"/>
Using the “do show ip interface brief” command, we can see that each interface is up and assigned an IP address. 
<br />
<br />
Note that Packet Tracer cannot actually connect to the internet, so R1 is not connected to a real ISP. G0/2 has an unassigned IP address, but in a real-world situation, it would have been automatically configured. 
<br />
<br />
Later on, I manually set R1’s IP address to match the 203.0.113.0 network of the ISP routers that I set up to act as the internet.
<br />
<br />
<img src="https://i.imgur.com/qUwopgW.png"/>
The DSW configurations follow. G1/0/1 and 2 on each DSW are connected to each other, so I bundle them together in Port-channel 1 again. With the “no switchport” command, Po1 now becomes a layer 3 link and I can assign it an IP address.
<br />
<br />
<img src="https://i.imgur.com/dc0tK37.png"/>
Using the “do show etherchannel summary” command, Po1 is now listed as a layer 3 port-channel instead of a layer 2 one. I successfully pinged 192.168.0.42, DSW2’s side of the link, confirming that there is connectivity.
<br />
<br />
<img src="https://i.imgur.com/vFStxXZ.png"/>
I made G1/0/3 a layer 3 connection using “no switchport” again and assigned it the IP address for R1’s point-to-point connection. Finally, I added the loopback interface.
<br />
<br />
<img src="https://i.imgur.com/TfH1gmC.png"/>
The ASW configurations follow. Each ASW has their default gateway set to 192.168.0.1 (located in the management VLAN). The management VLAN 99 is enabled on the switch so that we can assign an IP address to it.
<br />
<br />
<img src="https://i.imgur.com/52N2PaC.png"/>
On SRV1, the default gateway is set to 192.168.3.1 (located in the server VLAN).
<br />
<br />
<img src="https://i.imgur.com/IH1zzuH.png"/>
SRV1’s IP address is manually set to 192.168.3.4, and other devices will use this address as their DNS server.
<br />
<br />
<img src="https://i.imgur.com/FndErd5.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>9. Hot Standby Router Protocol (HSRP)</h3>
HSRP allows the use of a virtual IP address that either of the DSW can use. This is useful because each VLAN can have a different IP address that other devices can use as their default gateway. It also provides redundancy since the backup router can take over the active router if it goes down. Each HSRP group, subnet, and IP addresses are below.
<br />
<br />
<img src="https://i.imgur.com/eidYwk1.png"/>
The configurations on each DSW are the same, except one of them will be an active router and the other will be a standby router. The standby router uses the default priority of 100.
<br />
<br />
First, the DSW will be assigned its own IP address on the subnet. After, the virtual IP of the group that the active router uses (192.168.0.1 in this case) is assigned. A higher HSRP priority (I use 200 in this case) makes that specific switch the active router. Preemption ensures that this router will always be the active router whenever possible.
<br />
<br />
Group 1
<br />
<br />
<img src="https://i.imgur.com/QS2zRJP.png"/>
Group 2
<br />
<br />
<img src="https://i.imgur.com/ueWKZ0l.png"/>
Group 3
<br />
<br />
<img src="https://i.imgur.com/4VMVuMM.png"/>
Group 4
<br />
<br />
<img src="https://i.imgur.com/vhen528.png"/>
Group 5
<br />
<br />
<img src="https://i.imgur.com/KyBFOMi.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>10. Spanning Tree Protocol (STP)</h3>
STP is a layer 2 protocol that prevents loops and broadcast storms while providing network redundancy. In this case, I use the Cisco-proprietary Rapid PVST+ protocol.
<br />
<br />
Per VLAN Spanning Tree, or PVST, must be enabled on each VLAN. Like HSRP, a switch is elected as the root bridge depending on the switch’s priority. A switch with priority 0 has the highest priority, and a priority of 4096 (one increment higher than 0) makes that switch a secondary bridge in this case.
<br />
<br />
<img src="https://i.imgur.com/iai2Vtt.png"/>
DSW1 will be the root bridge for VLANs 99 and 10, and the secondary bridge for VLANs 20, 30, and 40. Using the “do show spanning-tree vlan (VLAN-ID)” command, we can see whether or not this bridge is the root in that VLAN.
<br />
<br />
<img src="https://i.imgur.com/EVCN5q0.png"/>
DSW2 will be the root bridge for VLANs 20, 30, and 40, and the secondary bridge for VLANs 99 and 10.
<br />
<br />
<img src="https://i.imgur.com/DEqAU2P.png"/>
PortFast enables computers or servers to instantly be able to use that specific port. Normally, a port must go through several STP states before it can be used. It is only enabled on access ports that connect to end devices. 
<br />
<br />
In addition, BPDU Guard is used in conjunction with PortFast to prevent switches or rogue devices from instantly being able to connect to the STP topology and cause network issues.
<br />
<br />
<img src="https://i.imgur.com/zTvLOE2.png"/>
Since F0/3 on ASW1 is connected to the WLC, it must be a trunk port. While you can normally only enable PortFast and BPDU Guard on access ports, you can use the “spanning-tree portfast trunk” command to bypass this.
<br />
<br />
<img src="https://i.imgur.com/1MifSRr.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>11. Open Shortest Path First (OSPF) and IPv4 Routes</h3>
OSPF is a dynamic routing protocol that shares routing information. Instead of statically configuring IP routes to every section of the network, routers and multilayer switches can dynamically share their routes with the rest of the autonomous system.
<br />
<br />
On R1, I start OSPF with process ID 1 and set R1’s router ID to the IP address of Loopback0. Since Loopback0 is not routable, it does not need to advertise itself. “passive-interface” disables OSPF advertisements on the specified interface.
<br />
<br />
I set area 0, the default (backbone) area, on each interface that OSPF is activated. Furthermore, G0/0 and G0/1 are configured as point-to-point since a designated router (DR) and backup designated router (BDR) are not needed for /30 links.
<br />
<br />
<img src="https://i.imgur.com/rneKnVA.png"/>
On both DSWs, the router ID is set to their respective Loopback0 IP addresses and Loopback0 is set to passive. On each interface, the “network” command is used to advertise the networks that fall within the specified range. Finally, G1/0/3 is set to point-to-point.
<br />
<br />
<img src="https://i.imgur.com/S188MVW.png"/>
Similar configurations are needed for each VLAN as well. I didn’t set VLAN 99 as passive since the management VLAN routes are what need to be shared across the network.
<br />
<br />
<img src="https://i.imgur.com/yE3Kd5f.png"/>
Using “do show ip ospf neighbor” we can see that R1 and both DSWs are all neighbors with each other.
<br />
<br />
<img src="https://i.imgur.com/YUG6NIL.png"/>
Using “do show ip route” we can see that OSPF routes are being shared on R1.
<br />
<br />
<img src="https://i.imgur.com/x3XGUzc.png"/>
OSPF routes are being shared on the DSWs too, and DSW1 can ping 203.0.113.2, R1’s internet-facing interface, even though I didn’t configure a route myself.
<br />
<br />
<img src="https://i.imgur.com/Nrfkha0.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>12. Dynamic Host Configuration Protocol (DHCP)</h3>
DHCP makes it possible to dynamically assign, or lease, IP addresses to devices on the network. Below are the DHCP pools that I configured for this project. Every VLAN except the 30, the server VLAN, gets a pool. SRV1’s IP address should stay the same, and I already configured it earlier.
<br />
<br />
<img src="https://i.imgur.com/Zq9PFFH.png"/>
On R1, I started by excluding the first 10 usable addresses in each subnet. Theoretically, I saved these addresses in case the network gets expanded and some devices need IP addresses that stay the same. 
<br />
<br />
Each DHCP subnet address matches the HSRP group subnets addresses. The default gateway of each subnet is the first usable address, the domain name is grilledonion.com, and the DNS server is SRV1’s IP address.
<br />
<br />
<img src="https://i.imgur.com/J6PCYM6.png"/>
On both DSWs, I used the “ip helper-address” command to define R1 as the DHCP server and the DSWs as the DHCP relay agent.
<br />
<br />
<img src="https://i.imgur.com/LT2MAMX.png"/>
On PC1, I used the “ipconfig /renew” command to get a new dynamically assigned IP address. I pinged R1’s loopback address and internet-facing interface, which were successful.
<br />
<br />
<img src="https://i.imgur.com/Ggfcat4.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>13. Domain Name System (DNS)</h3>
DNS translates IP addresses into more human-friendly readable names. For example, we can type “google.com” as the target of a ping instead of “8.8.8.8.”
<br />
<br />
On the DNS server, SRV1, I created an A record (for IPv4) that records the above translation. Furthermore, I created a CNAME called “www.google.com” that maps to “google.com.”
<br />
<br />
<img src="https://i.imgur.com/DzqLBSN.png"/>
Back on PC1, I pinged using the target “google.com” and it correctly translates to 8.8.8.8. This also happens when I use “www.google.com” as well. The requests are timing out since I haven’t configured NAT yet.
<br />
<br />
<img src="https://i.imgur.com/VqOlMPh.png"/>
On R1, I set the DNS server to SRV1’s IP address.
<br />
<br />
<img src="https://i.imgur.com/UrQblUh.png"/>
The pings show that DNS work on R1 as well.
<br />
<br />
<img src="https://i.imgur.com/W1kEONS.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>14. Network Time Protocol (NTP)</h3>
NTP lets network devices sync their clock together. On R1, I use the “ntp master” command to set it as an NTP server that the rest of the network will sync to. The “ntp server” command is used to sync R1 to another NTP server, which is a <a href="https://tf.nist.gov/tf-cgi/servers.cgi">NIST Internet Time server</a>.
<br />
<br />
An authentication key, “onion,” is created and trusted so that R1 and the DSWs can authenticate with each other for security.
<br />
<br />
<img src="https://i.imgur.com/kKCOUk6.png"/>
On the DSWs, the same authentication key commands are used in addition to setting R1 as their NTP server.
<br />
<br />
<img src="https://i.imgur.com/Iw0vEMA.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>15. Simple Network Management Protocol (SNMP)</h3>
SNMP collects information on network devices and lets you modify device behavior.
<br />
<br />
The only configuration needed to start SNMP is the “snmp-server” command with a community string and setting it to read only/read and write. In this case I use the string “SNMPonion” and set it to read only.
<br />
<br />
<img src="https://i.imgur.com/Ns78nIb.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>16. Syslog</h3>
Syslog stores information about events, errors, or system performance in the form of logs. I set SRV1 as the logging IP address, enabled notifications of all severity, and set the size of the local buffer (that will contain Syslog messages) to 8192 bytes.
<br />
<br />
<img src="https://i.imgur.com/7vbpRB3.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>17. File Transfer Protocol (FTP)</h3>
FTP enables file transfer between devices. SRV1 contains an update file for R1 that I’ll transfer over with FTP.
<br />
<br />
<img src="https://i.imgur.com/5oLcn5e.png"/>
On R1, I set the FTP username and password configured on SRV1. The “do copy ftp flash” command lets you specify the filename to transfer.
<br />
<br />
<img src="https://i.imgur.com/YzXg2xG.png"/>
After a while, the file finished transferring.
<br />
<br />
<img src="https://i.imgur.com/npZ9Cmq.png"/>
The new file, ending in “115-3.M4a.bin,” can be seen on R1’s flash now. I also had to delete the old file, ending in “151-4.M4.bin,” for the update to work.
<br />
<br />
<img src="https://i.imgur.com/LzJmb1O.png"/>
I used the “boot system flash:(filename)” command to specify the new file as the one to boot with. Before the update, R1’s version was 15.1.
<br />
<br />
<img src="https://i.imgur.com/9rrFMAt.png"/>
After restarting R1, the new version is 15.5.
<br />
<br />
<img src="https://i.imgur.com/auydq8o.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>18. Secure Shell (SSH) and Access Control Lists (ACLs)</h3>
SSH lets a device connect to another remote device and issue commands on it. During the SSH configuration, I use an ACL to restrict access to the PC subnet only.
<br />
<br />
“crypto key generate rsa” enables SSH and creates a key to be used for security reasons. I decided to go with a 4096-bit key. I set the SSH version to support version 2 only.
<br />
<br />
The “access-list” command creates the access list to permit only the PC subnet hosts to SSH into R1. All other IP addresses are implicitly and automatically denied.
<br />
<br />
The “line vty 0 15” command lets me configure the SSH settings on all possible console lines. I applied the ACL, restricted connections to SSH only, required login using local credentials, and enabled console messages.
<br />
<br />
Finally, I configured credentials, or secrets, on R1 to authenticate both local and SSH users.
<br />
<br />
<img src="https://i.imgur.com/rikZKnS.png"/>
PC1 can successfully SSH into R1.
<br />
<br />
<img src="https://i.imgur.com/ad9RXST.png"/>
SRV1 is not allowed to SSH into R1, meaning that the ACL was configured correctly.
<br />
<br />
<img src="https://i.imgur.com/RqW6rqq.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>19. Network Address Translation (NAT)</h3>
NAT translates internal IP addresses to public, internet-facing IP addresses. 
<br />
<br />
On R1, I set G0/2, which faces the ISP routers, as the outside NAT interface. G0/0 and 1, which face the network, are set as the inside NAT interfaces.
<br />
<br />
<img src="https://i.imgur.com/ykqhHZF.png"/>
Another ACL is created to let R1 know which addresses to translate. All VLAN traffic except the management VLAN should be translated.
<br />
<br />
<img src="https://i.imgur.com/i8lF6dd.png"/>
In this case, I decided to use NAT overload. In other words, multiple internal devices will share the same public IP address. The “ip nat pool” command is used to configure which range of IP addresses will be used for NAT.
<br />
<br />
The “ip nat inside source list (ACL) pool (poolname) overload” command enables NAT with the specified ACL and pool.
<br />
<br />
<img src="https://i.imgur.com/NX6kbip.png"/>
PC1 and SRV1 can now ping “google.com” successfully.
<br />
<br />
<img src="https://i.imgur.com/iXoE7zq.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>20. Link Layer Discovery Protocol (LLDP)</h3>
LLDP allows network devices to share information about themselves with other devices. I decided to configure LLDP, a vendor-neutral protocol, instead of CDP, Cisco’s proprietary protocol.
<br />
<br />
On R1 and the DSWs, the “no cdp run” command disables CDP and the “lldp run” command enables LLDP.
<br />
<br />
<img src="https://i.imgur.com/ZiQUmCL.png"/>
The ASWs also require that the access ports do not transmit LLDP information for security reasons.
<br />
<br />
<img src="https://i.imgur.com/zAVM3p3.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>21. Port Security</h3>
Port security restricts access to which devices can physically connect to the network. It only needs to be configured on the ASWs since only they have ports that end devices connect to. Port security is enabled per interface, and F0/2 is the only interface connected to an end device. 
<br />
<br />
The restrict violation mode permits traffic from known MAC addresses while dropping traffic from unknown MAC addresses and sending a warning message if a traffic violation occurs.
<br />
<br />
Sticky MAC addresses lets a switch learn and save a MAC address on a specific port.
<br />
<br />
<img src="https://i.imgur.com/cUPbfRr.png"/>
ASW2 has an IP phone and PC connected to it, so the maximum amount of MAC addresses it is allowed to learn must be set to 2.
<br />
<br />
<img src="https://i.imgur.com/iKGMBXk.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>22. DHCP Snooping</h3>
DHCP snooping prevents unauthorized DHCP servers from leasing IP addresses to DHCP clients. It can also limit how quickly DHCP messages can be received in one second.
<br />
<br />
DHCP snooping only needs to be enabled on switches (in this case, the ASWs) with end points connected to it. Trunk ports are usually trusted ports while access ports should be untrusted.
<br />
<br />
I enabled DHCP snooping globally and on all VLANs. “no ip dhcp snooping information option,” known as option 82, is a setting that sometimes causes issues in Packet Tracer, so I disabled it.
<br />
<br />
Once DHCP snooping is enabled, all ports are untrusted by default. Since F0/1 and 4 are trunk ports and connect to other switches, I trusted them. Finally, I limited the access ports to 15 packets per second. F0/3, which connects to the WLC, is an exception and is set to 100 packets per second.
<br />
<br />
<img src="https://i.imgur.com/WCi5xwI.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>23. Dynamic ARP Inspection (DAI)</h3>
DAI protects switches against ARP spoofing by inspecting ARP packets and validating them using the DHCP snooping database.
<br />
<br />
I enabled DAI on all VLANs and set it to validate ARP packets based on their source/destination MAC addresses and IP addresses.
<br />
<br />
Again, I set F0/1 and 4 to be trusted ports since they connect to the DSWs and are trunk ports.
<br />
<br />
<img src="https://i.imgur.com/igpzGP3.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>24. IPv6</h3>
Configuring IPv6 addresses is similar to configuring IPv4 addresses. 
<br />
<br />
To start, I enabled IPv6 on R1 with “ipv6 unicast-routing” and assigned G0/2’s IP address. I decided to use eui-64 to automatically configure an address for G0/0 and 1.
<br />
<br />
<img src="https://i.imgur.com/cF0m5wO.png"/>
I followed the same steps on the DSWs.
<br />
<br />
<img src="https://i.imgur.com/Jxh4ZVn.png"/>
Furthermore, I enabled IPv6 on Portchannel1 without assigning an IP address. In this case, it was fine to keep the automatically created loopback address for this interface.
<br />
<br />
<img src="https://i.imgur.com/37whEDs.png"/>
Finally, I added a default IPv6 route to R1 that specifies the ISP as the next hop.
<br />
<br />
<img src="https://i.imgur.com/MedsWNh.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>25. Wireless Networking</h3>
Thankfully, we’re finally getting around to the wireless network portion of the project. I set WLC1’s IP address to 192.168.0.7, a usable address on the management VLAN. The default gateway is set to the HSRP group’s virtual IP address, and the DNS server set to SRV1’s IP address.
<br />
<br />
<img src="https://i.imgur.com/j8v5LpR.png"/>
In the Wireless LANs tab, I created the Wi-Fi WLAN that uses VLAN 40, WPA2-PSK with the passphrase “grilledonion,” and AES encryption.
<br />
<br />
<img src="https://i.imgur.com/1C3tsjo.png"/>
In the AP Groups tab, I added LWAP1 as an access point in the Wi-Fi WLAN.
<br />
<br />
<img src="https://i.imgur.com/L0ZXkCO.png"/>
On Laptop1, I set it’s Wireless0 interface to join the network with the SSID Wi-Fi and passphrase that was just configured. Please note that Packet Tracer does not support IP address assignment through DHCP on wireless networks.
<br />
<br />
<img src="https://i.imgur.com/n2LoQX6.png"/>
Regardless, we can see in the network topology that Laptop1 has now associated with LWAP1.
<br />
<br />
<img src="https://i.imgur.com/RG5ECxs.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>26. Security</h3>
To finish off the project, I configured credentials on R1 and all the switches. Normally this step should be first, but for the purposes of this lab, I saved it for last so I didn’t have to constantly reauthenticate while making all the configurations.
<br />
<br />
On R1, I set the password “grilledonion” with type 5 encryption. The same was done for username and password “grilledonion.”
<br />
<br />
In the running-config we can see the secrets stored in encrypted form.
<br />
<br />
Afterwards, I required that login be used with local credentials, the session to be timed out after an hour of inactivity, and for console messages to not interrupt command input.
<br />
<br />
<img src="https://i.imgur.com/XG4SYZe.png"/>
On the DSWs, I followed the same steps but with type 9 encryption.
<br />
<br />
<img src="https://i.imgur.com/jqysUdz.png"/>
Finally, I followed the same steps on the ASWs but with default encryption.
<br />
<br />
<img src="https://i.imgur.com/U8xqFCv.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>Conclusion</h3>
With that, the configuration of the network is complete. I know this project is lengthy, but I wanted to document most of my steps and provide proof of my understanding of network concepts. 
<br />
<br />
If you made it this far, thank you for reading. Please make sure to check out my other projects that are listed on my <a href="https://github.com/rolandsalvador">homepage</a>!
<br />
<br />

[Back to top](#small-office-network-part-2---configuration)
