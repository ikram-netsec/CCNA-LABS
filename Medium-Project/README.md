School Network Infrastructure Project – VLANs, DHCP, DNS & Inter-VLAN Routing
Step 1: Subnetting
| Department     | Hosts | Network           | Mask            | Gateway        |
| -------------- | ----- | ----------------- | --------------- | -------------- |
| Computer Lab   | 50    | 192.168.100.0/26  | 255.255.255.192 | 192.168.100.1  |
| Teachers       | 30    | 192.168.100.64/27 | 255.255.255.224 | 192.168.100.65 |
| Administration | 20    | 192.168.100.96/27 | 255.255.255.224 | 192.168.100.97 |
Topology
R1
│
S1 ----- Computer Lab PCs
│
S2 ----- Teachers PCs
│
S3 ----- Administration PCs
│
DHCP/DNS Server
Router Configuration (Router-on-a-Stick)
enable
configure terminal

hostname R1

interface g0/0
no shutdown
exit

interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.100.1 255.255.255.192
exit

interface g0/0.20
encapsulation dot1Q 20
ip address 192.168.100.65 255.255.255.224
exit

interface g0/0.30
encapsulation dot1Q 30
ip address 192.168.100.97 255.255.255.224
exit

end
copy running-config startup-config
Switch Configuration (S1)
enable
configure terminal

hostname S1

vlan 10
name COMPUTER_LAB

vlan 20
name TEACHERS

vlan 30
name ADMINISTRATION

interface f0/1
switchport mode trunk

interface range f0/2-f0/16
switchport mode access
switchport access vlan 10
Switch Configuration (S2)
enable
configure terminal

interface range f0/2-f0/10
switchport mode access
switchport access vlan 20



The complete router and switch configurations
Verification commands (show commands)
A professional README for GitHub
Explanations of every configuration step


🟡 Medium Project – School Network
Scenario

A school has three departments:

Administration → 20 hosts
Teachers → 30 hosts
Computer Lab → 50 hosts
Requirements
1. Subnet the network

Network: 192.168.100.0/24

Create separate subnets.

2. Topology
1 Router
3 Switches
1 DHCP Server
15 PCs in Packet Tracer
3. Configure
DHCP for each department
Default gateways
Router interfaces
DNS server
4. Test
Ping between departments.
Access the school's website from PCs.
Concepts Covered

✅ Subnetting
✅ DHCP
✅ DNS
✅ Routing
✅ Application Layer
✅ ARP  


Perfect! This is a good medium-level ITN project. Below is a complete example configuration.

Step 1: Subnetting

Network: 192.168.100.0/24

Department	Hosts	Network	Mask	Gateway
Computer Lab	50	192.168.100.0/26	255.255.255.192	192.168.100.1
Teachers	30	192.168.100.64/27	255.255.255.224	192.168.100.65
Administration	20	192.168.100.96/27	255.255.255.224	192.168.100.97
Topology
R1
│
S1 ----- Computer Lab PCs
│
S2 ----- Teachers PCs
│
S3 ----- Administration PCs
│
DHCP/DNS Server
Router Configuration (Router-on-a-Stick)
enable
configure terminal

hostname R1

interface g0/0
no shutdown
exit

interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.100.1 255.255.255.192
exit

interface g0/0.20
encapsulation dot1Q 20
ip address 192.168.100.65 255.255.255.224
exit

interface g0/0.30
encapsulation dot1Q 30
ip address 192.168.100.97 255.255.255.224
exit

end
copy running-config startup-config
Switch Configuration (S1)
enable
configure terminal

hostname S1

vlan 10
name COMPUTER_LAB

vlan 20
name TEACHERS

vlan 30
name ADMINISTRATION

interface f0/1
switchport mode trunk

interface range f0/2-f0/16
switchport mode access
switchport access vlan 10
Switch Configuration (S2)
enable
configure terminal

interface range f0/2-f0/10
switchport mode access
switchport access vlan 20
Switch Configuration (S3)
enable
configure terminal

interface range f0/2-f0/7
switchport mode access
switchport access vlan 30
DHCP Server Configuration
Pool 1 – Computer Lab
Default Gateway: 192.168.100.1
DNS Server: 192.168.100.130
Start IP: 192.168.100.2
Subnet Mask: 255.255.255.192
Pool 2 – Teachers
Default Gateway: 192.168.100.65
DNS Server: 192.168.100.130
Start IP: 192.168.100.66
Subnet Mask: 255.255.255.224
Pool 3 – Administration
Default Gateway: 192.168.100.97
DNS Server: 192.168.100.130
Start IP: 192.168.100.98
Subnet Mask: 255.255.255.224
DNS Server

On the server:

IP Address: 192.168.100.130
Subnet Mask: 255.255.255.224
Default Gateway: 192.168.100.97

DNS Record:

school.com  → 192.168.100.130
www.school.com → 192.168.100.130
Enable the HTTP service on the server and create a simple webpage.

Verification Commands
show ip interface brief
show vlan brief
show interfaces trunk
show running-config
show ip route
Testing

From any PC:

ping 192.168.100.1
ping 192.168.100.65
ping 192.168.100.97
ping 192.168.100.130

Open the web browser and visit:

http://www.school.com
