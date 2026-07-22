# EtherChannel-PAgP-LACP-Lab

## Overview
This is a self-created CCNA Packet Tracer lab demonstrating the implementation of Cisco EtherChannel using all three supported methods:

- LACP (IEEE 802.3ad Standard)
- PAgP (Cisco Proprietary)
- Static EtherChannel (Mode On)

The lab focuses on link aggregation, redundancy, increased bandwidth, trunking, VLAN management, and Spanning Tree Protocol (STP) interaction.

---

# Topology

```
                  PC0
                   |
                VLAN 10
                   |
                 SW0
              /          \
       LACP             PAgP
        Po1              Po2
        ||               ||
       SW2=============SW1
         ||
      Static Po3
         ||
        SW3
         |
      VLAN 20
         |
        PC1
```

---

# Devices Used

- 4 × Cisco Catalyst 2960 Switches
- 2 × PCs
- Cisco Packet Tracer

---

# VLAN Configuration

| VLAN | Name |
|------|------|
| 10 | Sales |
| 20 | HR |
| 30 | IT |
| 99 | Native |

---

# EtherChannel Configuration

## Port-Channel 1
- Protocol: LACP
- Between: SW0 ↔ SW2
- Interfaces:
  - G0/1
  - G0/2

---

## Port-Channel 2
- Protocol: PAgP
- Between: SW0 ↔ SW1
- Interfaces:
  - F0/21
  - F0/22

---

## Port-Channel 3
- Protocol: Static EtherChannel
- Between: SW2 ↔ SW3
- Interfaces:
  - F0/23
  - F0/24

---

# Trunk Configuration

All Port-Channels are configured as trunk links.

Native VLAN

- VLAN 99

Allowed VLANs

- 10
- 20
- 30
- 99

---

# End Device Configuration

## PC0

- VLAN 10
- IP Address: 192.168.10.10/24

---

## PC1

- VLAN 20
- IP Address: 192.168.20.10/24

---

# Spanning Tree

- SW0 configured as Root Bridge
- STP recognizes each EtherChannel as a single logical link
- Redundant paths remain loop-free

---

# Verification Commands

```bash
show etherchannel summary

show interfaces trunk

show interfaces port-channel

show vlan brief

show spanning-tree

show lacp neighbor

show pagp neighbor
```

---

# Skills Demonstrated

- VLAN Configuration
- Trunk Configuration
- EtherChannel
- Link Aggregation
- LACP
- PAgP
- Static EtherChannel
- Port-Channel Configuration
- STP Optimization
- Redundancy
- Load Balancing
- Cisco IOS Verification
- Network Troubleshooting

---

# Technologies Used

- Cisco Packet Tracer
- Cisco IOS
- IEEE 802.3ad (LACP)
- Cisco PAgP
- Ethernet Switching
- Layer 2 Networking

---

## Author

**Ikram Ullah**

Software Engineering Student | CCNA | Network Security Enthusiast

This lab was independently designed and implemented as part of my CCNA hands-on practice to strengthen my practical networking and troubleshooting skills.
