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

<h3>1. Hostnames</h3>
a
<br />
<br />
<img src="https://i.imgur.com/Ge5T4b9.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>2. EtherChannel</h3>
a
<br />
<br />
<img src="https://i.imgur.com/2Wo4GgE.png"/>
<br />
<br />
<img src="https://i.imgur.com/SdEwSmQ.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>3. Trunk ports and Dynamic Trunking Protocol (DTP)</h3>
a
<br />
<br />
<img src="https://i.imgur.com/yImRKoN.png"/>
<br />
<br />
<img src="https://i.imgur.com/e2t6XFq.png"/>
<br />
<br />
<img src="https://i.imgur.com/CtOYsPj.png"/>
<br />
<br />
<img src="https://i.imgur.com/WcRcWtV.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>4. VLAN Trunking Protocol (VTP)</h3>
a
<br />
<br />
<img src="https://i.imgur.com/BJkJKgk.png"/>
<br />
<br />
<img src="https://i.imgur.com/IydGQCL.png"/>
<br />
<br />
<img src="https://i.imgur.com/X0Xv5Uo.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>5. Virtual Local Area Networks (VLANs)</h3>
a
<br />
<br />
<img src="https://i.imgur.com/obKl1r7.png"/>
<br />
<br />
<img src="https://i.imgur.com/R01U7Z7.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>6. Access ports</h3>
a
<br />
<br />
<img src="https://i.imgur.com/Rvud2tf.png"/>
<br />
<br />
<img src="https://i.imgur.com/yQsf8Gp.png"/>
<br />
<br />
<img src="https://i.imgur.com/V9FMFQX.png"/>
<br />
<br />
<img src="https://i.imgur.com/riob2RF.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>7. Disabling unused ports</h3>
a
<br />
<br />
<img src="https://i.imgur.com/IFBYVDy.png"/>
<br />
<br />
<img src="https://i.imgur.com/4FjGyUH.png"/>
<br />
<br />
<img src="https://i.imgur.com/lO70pwO.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>8. IPv4</h3>
a
<br />
<br />
<img src="https://i.imgur.com/v8DJwPz.png"/>
<br />
<br />
<img src="https://i.imgur.com/XmgU4SC.png"/>
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
a
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
a
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
a
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
a
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
a
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
a
<br />
<br />
<img src="https://i.imgur.com/kKCOUk6.png"/>
<br />
<br />
<img src="https://i.imgur.com/Iw0vEMA.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>15. Simple Network Management Protocol (SNMP)</h3>
a
<br />
<br />
<img src="https://i.imgur.com/Ns78nIb.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>16. Syslog</h3>
a
<br />
<br />
<img src="https://i.imgur.com/7vbpRB3.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>17. File Transfer Protocol (FTP)</h3>
a
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
a
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
a
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
a
<br />
<br />
<img src="https://i.imgur.com/ZiQUmCL.png"/>
<br />
<br />
<img src="https://i.imgur.com/zAVM3p3.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>21. Port Security</h3>
a
<br />
<br />
<img src="https://i.imgur.com/cUPbfRr.png"/>
<br />
<br />
<img src="https://i.imgur.com/iKGMBXk.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>22. DHCP Snooping</h3>
a
<br />
<br />
<img src="https://i.imgur.com/WCi5xwI.png"/>

[Back to top](#small-office-network-part-2---configuration)
  
<h3>23. Dynamic ARP Inspection (DAI)</h3>
a
<br />
<br />
<img src="https://i.imgur.com/igpzGP3.png"/>

[Back to top](#small-office-network-part-2---configuration)

<h3>24. IPv6</h3>
a
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
a
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
a
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
a

[Back to top](#small-office-network-part-2---configuration)
