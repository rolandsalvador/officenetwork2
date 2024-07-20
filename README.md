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

<br />
<br />
<img src="https://i.imgur.com/qUwopgW.png"/>

<br />
<br />
<img src="https://i.imgur.com/dc0tK37.png"/>

<br />
<br />
<img src="https://i.imgur.com/vFStxXZ.png"/>

<br />
<br />
<img src="https://i.imgur.com/TfH1gmC.png"/>

<br />
<br />
<img src="https://i.imgur.com/52N2PaC.png"/>

<br />
<br />
<img src="https://i.imgur.com/IH1zzuH.png"/>

<br />
<br />
<img src="https://i.imgur.com/FndErd5.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>9. Hot Standby Router Protocol (HSRP)</h3>

<br />
<br />
<img src="https://i.imgur.com/eidYwk1.png"/>

<br />
<br />
<img src="https://i.imgur.com/QS2zRJP.png"/>

<br />
<br />
<img src="https://i.imgur.com/ueWKZ0l.png"/>

<br />
<br />
<img src="https://i.imgur.com/4VMVuMM.png"/>

<br />
<br />
<img src="https://i.imgur.com/vhen528.png"/>

<br />
<br />
<img src="https://i.imgur.com/KyBFOMi.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>10. Spanning Tree Protocol (STP)</h3>

<br />
<br />
<img src="https://i.imgur.com/iai2Vtt.png"/>

<br />
<br />
<img src="https://i.imgur.com/EVCN5q0.png"/>

<br />
<br />
<img src="https://i.imgur.com/DEqAU2P.png"/>

<br />
<br />
<img src="https://i.imgur.com/zTvLOE2.png"/>

<br />
<br />
<img src="https://i.imgur.com/1MifSRr.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>11. Open Shortest Path First (OSPF) and IPv4 Routes</h3>

<br />
<br />
<img src="https://i.imgur.com/rneKnVA.png"/>

<br />
<br />
<img src="https://i.imgur.com/S188MVW.png"/>

<br />
<br />
<img src="https://i.imgur.com/yE3Kd5f.png"/>

<br />
<br />
<img src="https://i.imgur.com/YUG6NIL.png"/>

<br />
<br />
<img src="https://i.imgur.com/x3XGUzc.png"/>

<br />
<br />
<img src="https://i.imgur.com/Nrfkha0.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>12. Dynamic Host Configuration Protocol (DHCP)</h3>

<br />
<br />
<img src="https://i.imgur.com/Zq9PFFH.png"/>

<br />
<br />
<img src="https://i.imgur.com/J6PCYM6.png"/>

<br />
<br />
<img src="https://i.imgur.com/LT2MAMX.png"/>

<br />
<br />
<img src="https://i.imgur.com/Ggfcat4.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>13. Domain Name System (DNS)</h3>

<br />
<br />
<img src="https://i.imgur.com/DzqLBSN.png"/>

<br />
<br />
<img src="https://i.imgur.com/VqOlMPh.png"/>

<br />
<br />
<img src="https://i.imgur.com/UrQblUh.png"/>

<br />
<br />
<img src="https://i.imgur.com/W1kEONS.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>14. Network Time Protocol (NTP)</h3>

<br />
<br />
<img src="https://i.imgur.com/kKCOUk6.png"/>

<br />
<br />
<img src="https://i.imgur.com/Iw0vEMA.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>15. Simple Network Management Protocol (SNMP)</h3>

<br />
<br />
<img src="https://i.imgur.com/Ns78nIb.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>16. Syslog</h3>

<br />
<br />
<img src="https://i.imgur.com/7vbpRB3.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>17. File Transfer Protocol (FTP)</h3>

<br />
<br />
<img src="https://i.imgur.com/5oLcn5e.png"/>

<br />
<br />
<img src="https://i.imgur.com/YzXg2xG.png"/>

<br />
<br />
<img src="https://i.imgur.com/npZ9Cmq.png"/>

<br />
<br />
<img src="https://i.imgur.com/LzJmb1O.png"/>

<br />
<br />
<img src="https://i.imgur.com/9rrFMAt.png"/>

<br />
<br />
<img src="https://i.imgur.com/auydq8o.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>18. Secure Shell (SSH) and Access Control Lists (ACLs)</h3>

<br />
<br />
<img src="https://i.imgur.com/rikZKnS.png"/>

<br />
<br />
<img src="https://i.imgur.com/ad9RXST.png"/>

<br />
<br />
<img src="https://i.imgur.com/RqW6rqq.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>19. Network Address Translation (NAT)</h3>

<br />
<br />
<img src="https://i.imgur.com/ykqhHZF.png"/>

<br />
<br />
<img src="https://i.imgur.com/i8lF6dd.png"/>

<br />
<br />
<img src="https://i.imgur.com/NX6kbip.png"/>

<br />
<br />
<img src="https://i.imgur.com/iXoE7zq.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>20. Link Layer Discovery Protocol (LLDP)</h3>

<br />
<br />
<img src="https://i.imgur.com/ZiQUmCL.png"/>

<br />
<br />
<img src="https://i.imgur.com/zAVM3p3.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>21. Port Security</h3>

<br />
<br />
<img src="https://i.imgur.com/cUPbfRr.png"/>

<br />
<br />
<img src="https://i.imgur.com/iKGMBXk.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>22. DHCP Snooping</h3>

<br />
<br />
<img src="https://i.imgur.com/WCi5xwI.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>23. Dynamic ARP Inspection (DAI)</h3>

<br />
<br />
<img src="https://i.imgur.com/igpzGP3.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>24. IPv6</h3>

<br />
<br />
<img src="https://i.imgur.com/cF0m5wO.png"/>

<br />
<br />
<img src="https://i.imgur.com/Jxh4ZVn.png"/>

<br />
<br />
<img src="https://i.imgur.com/37whEDs.png"/>

<br />
<br />
<img src="https://i.imgur.com/MedsWNh.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>25. Wireless Networking</h3>

<br />
<br />
<img src="https://i.imgur.com/j8v5LpR.png"/>

<br />
<br />
<img src="https://i.imgur.com/1C3tsjo.png"/>

<br />
<br />
<img src="https://i.imgur.com/L0ZXkCO.png"/>

<br />
<br />
<img src="https://i.imgur.com/n2LoQX6.png"/>

<br />
<br />
<img src="https://i.imgur.com/RG5ECxs.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>26. Security</h3>

<br />
<br />
<img src="https://i.imgur.com/XG4SYZe.png"/>

<br />
<br />
<img src="https://i.imgur.com/jqysUdz.png"/>

<br />
<br />
<img src="https://i.imgur.com/U8xqFCv.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>Conclusion</h3>


[Back to top](#small-office-network-part-2---configuration)
