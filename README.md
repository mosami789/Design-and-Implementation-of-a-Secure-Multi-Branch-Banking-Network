🧱 Key Components:
1. Data Center (DC):
Hosts a central server (Server1) providing:
DNS, DHCP, NTP, Radius, Syslog-ng services.
Server is connected to vIOS-Ser-I using the internal subnet 172.16.50.0/24.
vIOS-Ser-I is connected to the firewall ASAv-I through interface Gi0/3.

2. Campus Network:
A hierarchical design including three layers:

🔹 Core Layer:
vIOS-Core-I and vIOS-Core-II are connected via OSPF Area 0.

🔹 Distribution Layer:
vEOS-Dis-I acts as the distribution switch and uses VRRP to provide high availability default gateways for VLANs.

🔹 Access Layer:
OpenSwitch-Acc-I and OpenSwitch-Acc-II connect end devices.

Hosts are segmented into different VLANs:
VLAN10: 192.168.10.0/24
VLAN20: 192.168.20.0/24
VLAN30: 192.168.30.0/24
VLAN40: 192.168.40.0/24
Each VLAN has its own IP range and virtual gateway using VRRP.

3. DMZ (Demilitarized Zone):
Contains a firewall (ASAv-DMZ-I) connected to the internet and to the internal DMZ router (vIOS-DMZ-I).
A public-facing server (Serv-DMZ-I) is located here, offering:
DNS, NTP, Web, and Syslog-ng services.
DMZ IP range is 195.1.1.160/29.

🌐 Internet Connectivity:
Handled by vIOS-EDGE-I, which connects to two ISPs:
ISP1 via 198.10.10.0/30 using eBGP (ASN 64501).
ISP2 via 197.10.10.0/30 using eBGP (ASN 64502).
Public IP block 195.1.1.0/25 is used for NAT.

🔐 Security Design:
Two firewalls (ASAv-I and ASAv-DMZ-I) are deployed:
One separates the internal network from the internet.
The other secures the DMZ zone.
The DMZ acts as a buffer zone to securely expose public services.

🔁 Protocols Used:
OSPF Area 0: For dynamic internal routing.
eBGP: For external internet connectivity via ISPs.
VRRP: For high availability default gateways per VLAN.
802.1Q: Used for VLAN trunking between switches and routers.

✅ Network Features:
Modular, scalable hierarchical design.
Redundant paths and high availability using VRRP.
Segmentation using VLANs.
Secure separation of internal, external, and public zones.
Support for dynamic routing and internet failover.
