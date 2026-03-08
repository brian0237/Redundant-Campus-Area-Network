# Redundant-Campus-Area-Network
This project demonstrates a redundant enterprise network based on the Cisco three-tier architecture (Core, Distribution, Access) The lab includes VLAN segmentation, inter-VLAN routing, OSPF, HSRP, EtherChannel, Rapid PVST+, ACLs, DHCP, DNS, NTP, SNMP, Syslog, FTP, SSH, NAT, and wireless connectivity.
# Network Topology
![Topology for the Campus Network](https://github.com/brian0237/Redundant-Campus-Area-Network/blob/c72173d19beac490374d0f92e5bc08a870c48135/Topology.png)
# Project Summary
This project simulates a highly available enterprise campus network connecting two office locations. The topology follows the Cisco three-tier architecture with redundant core switches, distribution switches, and access switches to ensure reliability and scalability. The network implements VLAN segmentation, inter-VLAN routing, and OSPF for dynamic routing between layers. High availability is achieved through HSRP, EtherChannel, and Rapid PVST+ to provide link and gateway redundancy. The design also integrates essential enterprise services such as DHCP, DNS, NTP, SNMP, Syslog, NAT, and secure management using SSH. Wireless connectivity is provided through a WLC and lightweight access points to support mobile devices across the network.
# Project Scenario
A company operates two offices, Office A and Office B, that require a reliable and scalable network to support data, voice, wireless users, and internal services. The network must ensure high availability and minimal downtime while allowing secure communication between departments and locations.

To achieve this, a redundant enterprise campus network was designed using the Cisco three-tier architecture (Core, Distribution, and Access layers). The network implements VLAN segmentation, inter-VLAN routing, dynamic routing, and redundancy mechanisms to maintain connectivity during link or device failures. Essential services such as DHCP, DNS, NAT, and network monitoring are also integrated to simulate a real-world enterprise environment.
# Technologies used
| Networking and switching | Services | Security | Routing | wireless |
|------------|-----|-------------|----------|---------|
| Cisco Catalyst 3650 multilayer switches     | DHCP Server  | SSH management access         |   OSPF       |  Wi-Fi DHCP pool        |
| Cisco Catalyst 2960 access switches        | FTP Server  | Standard ACL for VTY access      | Static Routing           |     PSK    |
| VLANs  | DNS Server  | Extended ACLs   |        ISP and Internet simulation   |  WPA2 wireless networks       |
| 802.1Q trunking      | Web server  | Inspection ACLs         |          |  WPA2 Policy with AES encryption        |
| Inter VLAN routing        | FTP  | IP arp inspection      |           |  Lightweight Access Points       |
|EtherChannel using LACP    | SMTP  | DHCP Snooping   |           |      SSIDs   |
| RSTP        | VoIP  | NAT and PAT      |           |         |
| HSRP  |   |    |           |         |
| BPDU Guard      |  |         |          |          |
|    VTP    |   |     |           |         |
|  DTP  |   | |           |         |
# Environment Setup 
## Software
Cisco Packet Tracer
## Devices Used
- 2 ISP Routers
- 1 Internal Router for routing and server for DNS and DHCP
- 2 Branch multilayer switches
- 4 Office multilayer switches
- 6 Office access switches
- 3 IP Phones
- 2 Lightweight Access points (LWAP)
- 1 Wireless LAN Controller (WLC)
- 3 PCs connected to the IP Phones
- 2 Laptops connected wirelessly to the LWAPs
- 1 Server for FTP and web
# Configurations made
## 1. Initial Setup
I configured appropriate hostnames for the routers and switches and also configures passwords and secrets to restrict access to the deices.
- Hostnames
- Passwords
- Synchronous Logging
## 2. VLANs and Layer 2 Eherchannel and trunking
I created VLANs to segment the network into logical broadcast domains to improve on security and traffic int the network.
VLANs used in the network:

1. VLAN 10: PCs
2. VLAN 20: Phones
3. VLAN 30: Servers
4. VLAN 40: Wi-Fi
5. VLAN 99: Management
   
I configured the following:
- Etherchannel PortChannel1 between the distribution switches in the various offices
- Set each trunk’s native VLAN to VLAN 1000 (unused)
- Disbled DTP
- Trunk and access ports on switch interfaces
Troubleshooting was done to resolve VLAN mismatches
# IP addresses, Layer-3 EtherChannel, HSRP

