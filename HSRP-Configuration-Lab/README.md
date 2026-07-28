
HSRP (Hot Standby Router Protocol) Configuration Lab
Project Overview

This project demonstrates the implementation of Hot Standby Router Protocol (HSRP), a Cisco proprietary First Hop Redundancy Protocol (FHRP) that provides default gateway redundancy in IPv4 networks. HSRP improves network reliability and availability by allowing multiple routers to function as a single virtual gateway. If the active router becomes unavailable, a standby router automatically assumes the gateway role, ensuring uninterrupted communication for end devices without requiring any configuration changes on the hosts.

This lab was designed and implemented using Cisco Packet Tracer as part of my CCNA v7 Enterprise Networking, Security, and Automation (ENSA) studies. It focuses on practical configuration, verification, troubleshooting, and failover testing of HSRP in a redundant network environment.

Objectives
Understand the purpose of First Hop Redundancy Protocols (FHRP).
Configure Hot Standby Router Protocol (HSRP).
Configure a Virtual IP (VIP) as the default gateway.
Configure HSRP Priority.
Configure HSRP Preemption.
Configure HSRP Version 2.
Understand Active and Standby router election.
Verify HSRP operation using Cisco IOS commands.
Perform failover testing.
Understand gateway redundancy and high availability.
Technologies Used
Cisco Packet Tracer
Cisco IOS
HSRP (Hot Standby Router Protocol)
FHRP (First Hop Redundancy Protocol)
IPv4 Addressing
Layer 3 Routing
High Availability (HA)
Gateway Redundancy
Key Concepts Covered

This lab covers several important CCNA networking concepts, including:

First Hop Redundancy Protocol (FHRP)
Hot Standby Router Protocol (HSRP)
Virtual Router
Virtual IP Address (VIP)
Virtual MAC Address (VMAC)
Active Router
Standby Router
HSRP Priority
HSRP Preemption
HSRP Timers
Active Router Election
Automatic Failover
Gateway Redundancy
Network High Availability
Cisco IOS Verification Commands
Network Topology

The topology consists of:

Two Cisco routers
One Layer 2 switch
Multiple end devices (PCs)
Shared Virtual IP Address
Redundant default gateway

The routers are configured in an HSRP group where:

One router operates as the Active Router
One router operates as the Standby Router
Both routers share a Virtual IP Address
End devices use only the Virtual IP as their default gateway
Features Implemented
Interface Configuration
IPv4 Address Configuration
HSRP Version 2
Virtual Gateway Configuration
Active Router Election
Standby Router Configuration
Priority Configuration
Preemption Configuration
Hello and Hold Timers
Automatic Gateway Failover
Network Redundancy
High Availability Design
Connectivity Verification
Verification Performed

The following Cisco IOS commands were used to verify the configuration:

show standby
show standby brief
show ip interface brief
show ip route
show arp
show running-config

Verification confirmed:

Active Router Status
Standby Router Status
Virtual IP Address
Virtual MAC Address
HSRP Priority
Router Election
Gateway Reachability
Successful Failover
Failover Testing

A failover test was performed by shutting down the interface of the Active Router.

During testing:

The Standby Router detected the failure.
It automatically transitioned to the Active state.
The Virtual IP Address remained unchanged.
End devices continued forwarding traffic without changing their default gateway.
Network connectivity was maintained throughout the failover process.

After restoring the original router, the Preempt feature allowed the higher-priority router to automatically reclaim the Active role.

Learning Outcomes

After completing this lab, I gained practical experience with:

Cisco First Hop Redundancy Protocols
HSRP Configuration
Gateway Redundancy
Virtual Gateway Concepts
Router Redundancy
Active and Standby Router Election
High Availability Network Design
Enterprise Network Reliability
Cisco IOS Verification
Troubleshooting HSRP
Failover and Recovery Testing
                    Internet
                        |
                -----------------
                |               |
              R1               R2
      192.168.1.2        192.168.1.3
          Active          Standby
                \         /
                 \       /
                  Switch
                     |
              ----------------
              |              |
             PC1            PC2

Virtual Gateway (HSRP)
IP Address : 192.168.1.1

IP Addressing Table
Device	Interface	IP Address	Subnet Mask
R1	G0/0	192.168.1.2	255.255.255.0
R2	G0/0	192.168.1.3	255.255.255.0
PC1	NIC	192.168.1.10	255.255.255.0
PC2	NIC	192.168.1.20	255.255.255.0
Virtual Gateway	HSRP	192.168.1.1	255.255.255.0
Router R1 Configuration
enable

configure terminal

hostname R1

interface GigabitEthernet0/0
 ip address 192.168.1.2 255.255.255.0
 no shutdown

 standby version 2
 standby 1 ip 192.168.1.1
 standby 1 priority 110
 standby 1 preempt

exit

end

write memory
Router R2 Configuration
enable

configure terminal

hostname R2

interface GigabitEthernet0/0
 ip address 192.168.1.3 255.255.255.0
 no shutdown

 standby version 2
 standby 1 ip 192.168.1.1
 standby 1 priority 100
 standby 1 preempt

exit

end


 
