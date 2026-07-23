# Enterprise Network Infrastructure Lab Configuration

## Project Overview

This lab demonstrates the implementation of an enterprise-style network using Cisco Packet Tracer. The network integrates centralized DHCP services, DHCP Relay, static routing, EtherChannel, Spanning Tree Protocol (STP), wireless connectivity, packet capture, and multiple LAN segments.

---

# Technologies Implemented

- Cisco Packet Tracer
- Enterprise Network Design
- Multi-Router Topology
- Multi-Switch Topology
- Static Routing
- Centralized DHCP Server
- DHCP Relay Agent (ip helper-address)
- EtherChannel
  - PAgP
  - LACP
- Spanning Tree Protocol (STP)
- Wireless Networking
- Packet Capture (Sniffer)
- Multiple LANs
- Server Farm
- End-to-End Connectivity Testing

---

# Network Segments

LAN 1 : 15.0.0.0/8

LAN 2 : 10.0.0.0/8

LAN 3 : 12.0.0.0/8

DHCP Relay Network : 11.0.0.0/8

Server Network : 13.0.0.0/8

Router Interconnection : 14.0.0.0/8

---

# Routing

- Static Routing
- End-to-End Connectivity
- Gateway Configuration
- Route Verification

Verification Commands

show ip route

ping

traceroute

---

# DHCP Configuration

Centralized DHCP Server

Configured Multiple DHCP Pools

Pool R1-LAN

Network : 15.0.0.0/8

Default Gateway : 15.0.0.1

DNS : 8.8.8.8

Domain Name : www.facebook.com

Pool R2-LAN

Network : 10.0.0.0/8

Default Gateway : 10.0.0.1

DNS : 8.8.8.8

Domain Name : www.facebook.com

Pool R3-LAN

Network : 12.0.0.0/8

Default Gateway : 12.0.0.1

DNS : 8.8.8.8

Domain Name : www.facebook.com

Excluded Address Ranges

15.0.0.1 - 15.0.0.10

10.0.0.1 - 10.0.0.10

12.0.0.1 - 12.0.0.10

Verification Commands

show ip dhcp binding

show ip dhcp pool

show ip dhcp server statistics

show ip dhcp conflict

---

# DHCP Relay Agent

Configured using

ip helper-address

Relay Forwarding

Client

↓

Relay Router

↓

Central DHCP Server

↓

DHCP Offer

↓

Relay Router

↓

Client

---

# Switching

Configured Cisco Catalyst 2960 Switches

Access Ports

Switch-to-Switch Connections

Redundant Links

---

# EtherChannel

Configured PAgP

Configured LACP

Load Balancing

Link Redundancy

Verification

show etherchannel summary

show interfaces trunk

---

# Spanning Tree Protocol

Configured STP

Verified Root Bridge

Prevented Layer 2 Loops

Captured BPDU Packets

Verification

show spanning-tree

show spanning-tree root

---

# Wireless Network

HomeRouter-PT-AC

Wireless Clients

Laptop

Smartphones

Wireless Access

DHCP Address Assignment

---

# Packet Capture

Cisco Packet Tracer Sniffer

Captured

- STP BPDUs
- DHCP Packets
- ICMP Packets

Protocol Analysis Performed

Layer 2

Layer 3

DHCP Exchange

STP Operation

---

# Servers

Multiple Servers

DHCP Services

DNS Configuration

Network Services

---

# Verification

Successful DHCP Lease

Successful Routing

Successful End-to-End Ping

Successful Wireless Connectivity

Successful EtherChannel

Successful STP Operation

Successful Packet Capture Analysis

---

# Troubleshooting Performed

DHCP clients received APIPA addresses.

Root Cause

The DHCP server lacked static routes to the client LANs.

Solution

Configured static routes on the DHCP server router.

Result

DHCP Relay successfully forwarded requests and clients received valid IPv4 addresses.

---

# Learning Outcomes

✔ Enterprise Network Design

✔ DHCP Server Configuration

✔ DHCP Relay Configuration

✔ Static Routing

✔ EtherChannel (PAgP & LACP)

✔ Spanning Tree Protocol

✔ Wireless Networking

✔ Packet Capture Analysis

✔ Network Troubleshooting

✔ End-to-End Connectivity Verification
