HSRP Configuration Lab demonstrates the implementation of Hot Standby Router Protocol (HSRP) in Cisco Packet Tracer. In this lab, I configured Active and Standby routers, a virtual gateway IP, priority, and preemption to provide gateway redundancy and ensure continuous network availability in case of a router failure. This lab strengthened my understanding of First Hop Redundancy Protocols (FHRP) and high-availability networking concepts as part of my CCNA studies.
R1 Configuration (Active Router)
enable
configure terminal

hostname R1

interface GigabitEthernet0/0
 ip address 10.1.1.1 255.255.255.252
 no shutdown

interface GigabitEthernet0/1
 ip address 192.168.1.1 255.255.255.0
 standby version 2
 standby 1 ip 192.168.1.254
 standby 1 priority 150
 standby 1 preempt
 no shutdown

interface GigabitEthernet0/2
 ip address 10.1.1.9 255.255.255.252
 no shutdown
R2 Configuration
enable
configure terminal

hostname R2

interface GigabitEthernet0/0
 ip address 10.1.1.2 255.255.255.252
 no shutdown

interface GigabitEthernet0/1
 ip address 10.1.1.5 255.255.255.252
 no shutdown

interface GigabitEthernet0/2
 ip address 10.100.100.1 255.255.255.252
 no shutdown

end
write memory
R3 Configuration (Standby Router)
enable
configure terminal

hostname R3

interface GigabitEthernet0/0
 ip address 192.168.1.3 255.255.255.0
 standby version 2
 standby 1 ip 192.168.1.254
 no shutdown

interface GigabitEthernet0/1
 ip address 10.1.1.6 255.255.255.252
 no shutdown

interface GigabitEthernet0/2
 ip address 10.1.1.10 255.255.255.252
 no shutdown

end
write memory
S1 Configuration
enable
configure terminal

hostname S1

interface vlan 1
 ip address 192.168.1.11 255.255.255.0
 no shutdown

ip default-gateway 192.168.1.254

end
write memory
S3 Configuration
enable
configure terminal

hostname S3

interface vlan 1
 ip address 192.168.1.13 255.255.255.0
 no shutdown

ip default-gateway 192.168.1.254

end
write memory

Today 11:29 AM

9.3.3-packet-tracer---hsrp-configuration-guide.pka
File
gave me full configuration of it plz 


9.3.3-packet-tracer---hsrp-configuration-guide.pdf
PDF

9.3.3-packet-tracer---hsrp-configuration-guide(1).pka
File
 i provide both pdf and all  now gave it

Based on the Cisco Packet Tracer HSRP Configuration Guide you uploaded, the required HSRP configuration is only on R1 and R3. The addressing table and required commands are defined in the guide. 


R1 Configuration (Active Router)
enable
configure terminal

hostname R1

interface GigabitEthernet0/0
 ip address 10.1.1.1 255.255.255.252
 no shutdown

interface GigabitEthernet0/1
 ip address 192.168.1.1 255.255.255.0
 standby version 2
 standby 1 ip 192.168.1.254
 standby 1 priority 150
 standby 1 preempt
 no shutdown

interface GigabitEthernet0/2
 ip address 10.1.1.9 255.255.255.252
 no shutdown

end
write memory
R2 Configuration
enable
configure terminal

hostname R2

interface GigabitEthernet0/0
 ip address 10.1.1.2 255.255.255.252
 no shutdown

interface GigabitEthernet0/1
 ip address 10.1.1.5 255.255.255.252
 no shutdown

interface GigabitEthernet0/2
 ip address 10.100.100.1 255.255.255.252
 no shutdown

end
write memory
R3 Configuration (Standby Router)
enable
configure terminal

hostname R3

interface GigabitEthernet0/0
 ip address 192.168.1.3 255.255.255.0
 standby version 2
 standby 1 ip 192.168.1.254
 no shutdown

interface GigabitEthernet0/1
 ip address 10.1.1.6 255.255.255.252
 no shutdown

interface GigabitEthernet0/2
 ip address 10.1.1.10 255.255.255.252
 no shutdown

end
write memory
S1 Configuration
enable
configure terminal

hostname S1

interface vlan 1
 ip address 192.168.1.11 255.255.255.0
 no shutdown

ip default-gateway 192.168.1.254

end
write memory
S3 Configuration
enable
configure terminal

hostname S3

interface vlan 1
 ip address 192.168.1.13 255.255.255.0
 no shutdown

ip default-gateway 192.168.1.254

end
write memory
PC Configuration
PC-A
IP Address : 192.168.1.101
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.254
PC-B
IP Address : 192.168.1.103
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.254
Verification Commands
show standby

show standby brief

show ip interface brief

show running-config

show ip route

ping 209.165.200.226

tracert 209.165.200.226
Expected Result
HSRP Version: 2
HSRP Group: 1
Virtual IP: 192.168.1.254
Active Router: R1
Standby Router: R3
R1 Priority: 150
R3 Priority: 100 (default)
Preempt: Enabled on R1, Disabled on R3
end
write memory
