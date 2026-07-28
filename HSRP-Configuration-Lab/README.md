Project Overview

This lab demonstrates how to configure Hot Standby Router Protocol (HSRP) to provide default gateway redundancy. HSRP ensures that if the primary gateway fails, a backup router automatically takes over, allowing hosts to maintain network connectivity without changing their default gateway.

Objectives
Configure HSRP between two Cisco routers.
Configure a Virtual IP Address.
Configure HSRP Priority.
Enable HSRP Preemption.
Verify Active and Standby routers.
Test automatic failover.
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

write memory
PC Configuration
PC1
IP Address: 192.168.1.10

Subnet Mask: 255.255.255.0

Default Gateway: 192.168.1.1
PC2
IP Address: 192.168.1.20

Subnet Mask: 255.255.255.0

Default Gateway: 192.168.1.1
HSRP Configuration Commands Explained
Command	Description
standby version 2	Enables HSRP Version 2
standby 1 ip 192.168.1.1	Creates Virtual Gateway
standby 1 priority 110	Sets router priority
standby 1 preempt	Allows higher priority router to reclaim Active role
Verification Commands
Verify HSRP
show standby
Brief Verification
show standby brief
Verify Interface
show ip interface brief
Verify Routing Table
show ip route
Verify ARP Table
show arp
HSRP Election Process
Highest Priority wins.
Default Priority is 100.
Highest IP address wins if priorities are equal.
Active router forwards traffic.
Standby router monitors the Active router.
Upon Active router failure, the Standby router immediately assumes the Active role.
HSRP States
State	Description
Initial	HSRP process starts
Learn	Virtual IP not yet learned
Listen	Receives HSRP Hello messages
Speak	Sends and receives Hello messages
Standby	Backup router
Active	Forwarding router
