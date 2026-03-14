# Redundant-Campus-Area-Network
This project demonstrates a redundant enterprise network based on the Cisco three-tier architecture (Core, Distribution, Access) The lab includes VLAN segmentation, inter-VLAN routing, OSPF, HSRP, EtherChannel, Rapid PVST+, ACLs, DHCP, DNS, NTP, SNMP, Syslog, FTP, SSH, NAT, and wireless connectivity.
# Network Topology
![Topology for the Campus Network](https://github.com/brian0237/Redundant-Campus-Area-Network/blob/9ae5ae90cd0e6595c2e45289af4755d4a8dd0a95/CampusNetworktopology.png)
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
# 3. IP addresses, Layer-3 EtherChannel, HSRP
I configured:
- DHCP on the internal router's interfaces
- Ip addresses for interfaces on the Core and distribution layer multilayer switches
- EtherChannel on the core and distribution layer switches
- The server's Default gateway, IPV4 address, and subnet mask
- Management IP addresses on the Access layer switches
- HSRPv2 for redundancy on the Distribution layer switches
All these configurations provided the network with link redundancy, increased bandwidth, load balancing
# Rapid Spanning Tree Protocol (RSTP)
I configured PVST+ on all Access and distribution Layer switches to prevent switching loops and to drastically reduce network convergence time from 50s (max age timer plus foward delay timer)to a few seconds. I did the following
- Enabled Portfast on all edge ports
- Enabled BPDU guard on edge ports to protect the spanning tree topology from external BPDU'S that could threaten the intergrit of the topology
# Static and Dynamic Routing
Configure OSPF on the internal router (LAN-facing interfaces) and all Core and Distribution switches (all Layer-3 interfaces)
I configured:
- all the devices in area 0
- Each device's RID to match the loopback interface
- OSPF on all loopback interfaces
- all physical connections between OSPF neighbors to use a network type that doesn’t elect a DR/BDR (Point to point)
- one static default route for each of the internal router's Internet connections. Made them recursive routes.
- the internal router to function as an OSPF ASBR and advertise itss default route to other routes in the OSPF domain.
# Network Services
I configured the following network services;
DHCP, DNS, NTP, SNMP, Syslog, FTP, SSH, NAT
For the DHCP pools, I created the management pool, PC pool, Phone pool, and a Wi-Fi pool. 
I configured:
- the Distribution switches to relay wired DHCP clients’ broadcast messages to the internal router’s Loopback0 IP address
- all routers and switches to use domain name jeremysitlab.com and used SRV1 as their DNS server.
- All Core, Distribution, and Access switches to use the internal router’s loopback interface as their NTP server
-  the SNMP community string SNMPSTRING on all routers and switches.
-  SSH for secure remote access on all routers and switches.
-  static NAT on R1 to enable hosts on the Internet to access SRV1
-  Disable CDP on all devices and enable LLDP instead.
# Security: ACLs and Layer-2 Security Features
I configured ACLs layer-2 security features like Port Security, DHCP snooping, and Dynamic ARP inspection to keep the network secure, enforce privacy and restrict access.
# IPv6
- To prepare for a migration to IPv6, I enabled IPv6 routing and configured IPv6 addresses on the internal router, CSW1, and CSW2
- I Configured two default static routes on the internal Router
# Wireless
I configured the following:
- A username and Password to restrict access to the GUI of the WLC1
- A dynamic interface for the Wi-Fi WLAN
- And enabled the following WLAN; Profile name, SSID, ID, Status, Security: WPA2 Policy with AES encryption, PSK
# Troubleshooting I did in the course of this project
1. OSPF Neighbor Adjacency Issue
I encountered a problem where OSPF neighbors were not forming between the core and distribution routers, which I resolved by correcting the OSPF network statements and ensuring both interfaces were in the same area.
2. HSRP Gateway Redundancy Failure
I noticed that hosts were unable to use the standby gateway during failover, which I fixed by adjusting the HSRP priority and verifying the correct virtual IP configuration.
3. VLAN Communication Problem
I faced an issue where devices in the same VLAN could not communicate across switches, which I resolved by allowing the VLANs on the trunk links between switches.
4. EtherChannel Not Forming
I observed that the links between switches were not bundling into an EtherChannel, and I fixed the issue by ensuring both sides had matching channel group configurations and interface settings.
5. Spanning Tree Root Bridge Misconfiguration
I discovered that traffic was taking inefficient paths due to an incorrect root bridge selection, which I corrected by manually setting the intended distribution switch as the STP root.
6. DHCP Address Assignment Failure
I encountered a situation where client devices were not receiving IP addresses, which I fixed by correcting the DHCP pool configuration and verifying the default gateway settings.
7. SSH Remote Management Access Issue
I initially could not access some network devices remotely via SSH, which I resolved by configuring the correct VTY line settings, enabling SSH, and verifying user authentication.
# Verification Commands
## 1. PCs
- ipconfig /all
- ping
## 2. Switches
- show cdp neighbors
- show spanning-tree
- show etherchannel summary
- show vlan brief
- show interface trunk
- show interface status
## 3. Routers
- show ip interface brief
- show ip route
- show ip ospf neighbor
# Skills acquired Applied in this lab
- Enterprise Network Design: Designed a scalable campus network using the Cisco three-tier architecture (Core, Distribution, Access).
- VLAN Segmentation:  Configured VLANs to logically separate departments and improve network organization.
- Inter-VLAN Routing: Implemented Layer 3 routing to allow communication between different VLANs.
- Dynamic Routing (OSPF): Configured OSPF to enable automatic route exchange between network devices.
- First Hop Redundancy (HSRP): Implemented gateway redundancy to ensure continuous network availability.
- Link Aggregation (EtherChannel): Configured EtherChannel to increase bandwidth and provide link redundancy.
- Spanning Tree Optimization (Rapid PVST+): Optimized Layer 2 redundancy while preventing switching loops.
- Network Services Deployment Configured DHCP, DNS, NTP, SNMP, Syslog, FTP, and NAT services.
- Wireless Network Integration: Implemented wireless connectivity using a WLC and access points.
- Network Security: Applied ACLs and secure device management using SSH.
- Network Monitoring and Troubleshooting: Diagnosed and resolved connectivity issues using Cisco verification commands.
# Future Improvements
## 1. Network Automation
The network could be enhanced by implementing automation using tools such as Python or Ansible to automate configuration deployment and reduce manual configuration errors.
## 2. Centralized Network Monitoring
A centralized monitoring platform such as PRTG, Grafana, or SolarWinds could be integrated to provide real-time visibility into network performance and device health.
## 3. IPv6 Implementation
The network could be expanded to support IPv6 addressing and dual-stack routing to prepare the infrastructure for modern networking requirements.
## 4. Network Segmentation with VRFs
Virtual Routing and Forwarding (VRF) could be implemented to further isolate network segments and improve scalability in larger enterprise environments.

# Recreating this project
Requirements

- Cisco Packet Tracer
- The .pkt project file
Steps

1. Open the Packet Tracer .pkt file.
2. Wait for devices to fully boot.
3. Check green link status and device convergence.
4. Use verification commands on switches, routers.
5. Test connectivity with pings and browser access.






