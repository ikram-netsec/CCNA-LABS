# CCNA Enterprise Network Implementation

##  Project Overview

This project demonstrates a complete Cisco CCNA Enterprise Network implemented in Cisco Packet Tracer. The topology integrates multiple routing and switching technologies to simulate a real-world enterprise network. The objective is to provide secure communication between multiple departments while implementing dynamic routing, VLAN segmentation, DHCP services, and inter-VLAN communication.

---

## Objectives

- Design a scalable enterprise network.
- Configure VLANs for network segmentation.
- Implement Inter-VLAN Routing.
- Configure DHCP for automatic IP address assignment.
- Configure Dynamic Routing.
- Verify end-to-end connectivity.
- Apply Cisco networking best practices.

---

##  Technologies Used

- Cisco Packet Tracer
- Cisco Routers
- Cisco Layer 2 Switches
- Cisco Layer 3 Switch
- VLAN
- IEEE 802.1Q Trunking
- Router-on-a-Stick
- DHCP
- OSPF
- RIP Version 2
- Static Routing
- IPv4 Addressing

---

# Network Features

 VLAN Configuration

 Access Ports
 
 Trunk Ports

 Router-on-a-Stick

 Inter-VLAN Routing

 DHCP Server

 Dynamic Routing (OSPF)

 Dynamic Routing (RIP v2)

 Static Routes

 End-to-End Connectivity Testing

---

# Configuration

## Router Configuration

```cisco
enable
configure terminal

hostname R1

interface GigabitEthernet0/0
ip address 10.0.0.1 255.255.255.0
no shutdown

interface GigabitEthernet0/1
no shutdown

interface GigabitEthernet0/1.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface GigabitEthernet0/1.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0

interface GigabitEthernet0/1.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0

interface GigabitEthernet0/1.40
encapsulation dot1Q 40
ip address 192.168.40.1 255.255.255.0

interface Serial0/0/0
ip address 11.0.0.1 255.255.255.252
clock rate 64000
no shutdown

router ospf 1
network 10.0.0.0 0.0.0.255 area 0
network 11.0.0.0 0.0.0.3 area 0
network 192.168.10.0 0.0.0.255 area 0
network 192.168.20.0 0.0.0.255 area 0
network 192.168.30.0 0.0.0.255 area 0
network 192.168.40.0 0.0.0.255 area 0

router rip
version 2
no auto-summary
network 11.0.0.0
network 20.0.0.0

ip dhcp excluded-address 192.168.10.1 192.168.10.20
ip dhcp excluded-address 192.168.20.1 192.168.20.20
ip dhcp excluded-address 192.168.30.1 192.168.30.20
ip dhcp excluded-address 192.168.40.1 192.168.40.20

ip dhcp pool VLAN10
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 8.8.8.8

ip dhcp pool VLAN20
network 192.168.20.0 255.255.255.0
default-router 192.168.20.1
dns-server 8.8.8.8

ip dhcp pool VLAN30
network 192.168.30.0 255.255.255.0
default-router 192.168.30.1
dns-server 8.8.8.8

ip dhcp pool VLAN40
network 192.168.40.0 255.255.255.0
default-router 192.168.40.1
dns-server 8.8.8.8

end
write memory
```

---

## Switch Configuration

```cisco
enable
configure terminal

hostname SW1

vlan 10
name HR

vlan 20
name SALES

vlan 30
name IT

vlan 40
name MANAGEMENT

interface range FastEthernet0/1-10
switchport mode access
switchport access vlan 10

interface range FastEthernet0/11-15
switchport mode access
switchport access vlan 20

interface range FastEthernet0/16-20
switchport mode access
switchport access vlan 30

interface range FastEthernet0/21-24
switchport mode access
switchport access vlan 40

interface GigabitEthernet0/1
switchport mode trunk

interface GigabitEthernet0/2
switchport mode trunk

end
write memory
```

---

# Verification Commands

```cisco
show ip interface brief

show vlan brief

show interfaces trunk

show ip route

show ip ospf neighbor

show ip protocols

show ip dhcp binding

show ip dhcp pool

show running-config

ping

traceroute
```

---

# Skills Demonstrated

- Enterprise Network Design
- VLAN Configuration
- Router-on-a-Stick
- DHCP Configuration
- OSPF Routing
- RIP Version 2
- Static Routing
- IPv4 Addressing
- Cisco CLI
- Network Troubleshooting
- Connectivity Verification

---

# Learning Outcomes

This project strengthened my understanding of Cisco Enterprise Networking by integrating routing, switching, VLANs, DHCP, and dynamic routing protocols into a single scalable topology. It provided hands-on experience in designing, configuring, verifying, and troubleshooting an enterprise network using Cisco Packet Tracer.

---

## Author

**Ikram Ullah**

BS Software Engineering

University of Malakand

Cisco Networking Academy Student

Aspiring Network Security Engineer

---

⭐ If you found this project helpful, consider giving this repository a star.
