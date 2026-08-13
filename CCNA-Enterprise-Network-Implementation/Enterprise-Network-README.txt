Completed the end-to-end implementation of a CCNA Enterprise Network project in Cisco Packet Tracer. Configured routers, Layer 3 core and distribution switches, access switches, VLANs, trunking, inter-VLAN routing, static routing, DHCP, DHCP relay, IPv6 (SLAAC, Stateless and Stateful DHCPv6), SSH, EtherChannel, Rapid PVST+, Port Security, DHCP Snooping, Dynamic ARP Inspection, and wireless network integration. Also organized the complete CLI configurations and project documentation for version control
total CLI configuration of this project 
2 (Cisco 3560 Multilayer Switch)
enable
configure terminal

hostname CORE2

no ip domain-lookup
service password-encryption

enable secret Cisco123

banner motd #
AUTHORIZED USERS ONLY
#

ip domain-name enterprise.local

username admin privilege 15 secret Cisco123

crypto key generate rsa
1024

ip ssh version 2

line console 0
 password cisco
 login
 logging synchronous
exit

line vty 0 15
 login local
 transport input ssh
exit

!
! Enable Layer 3 Routing
!
ip routing

!
! VLANs
!
vlan 10
 name MANAGEMENT
vlan 20
 name HR
vlan 30
 name FINANCE
vlan 40
 name SALES
vlan 50
 name IT
vlan 60
 name SERVER
vlan 70
 name PRINTER
vlan 80
 name GUEST_WIFI
vlan 90
 name EMPLOYEE_WIFI
vlan 99
 name NATIVE
exit

!
! SVI Interfaces
!

interface vlan10
 ip address 192.168.10.2 255.255.255.0
 no shutdown

interface vlan20
 ip address 192.168.20.2 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown

interface vlan30
 ip address 192.168.30.2 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown

interface vlan40
 ip address 192.168.40.2 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown

interface vlan50
 ip address 192.168.50.2 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown

interface vlan60
 ip address 192.168.60.2 255.255.255.0
 no shutdown

interface vlan70
 ip address 192.168.70.2 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown

interface vlan80
 ip address 192.168.80.2 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown

interface vlan90
 ip address 192.168.90.2 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown

!
! Routed Port to HQ Router
!
interface GigabitEthernet0/1
 no switchport
 ip address 10.0.1.6 255.255.255.252
 no shutdown

!
! EtherChannel to CORE1
!
interface range GigabitEthernet0/2-3
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,60,70,80,90,99
 channel-group 1 mode active
 no shutdown
exit

!
! Port-Channel Interface
!
interface Port-channel1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,60,70,80,90,99
 no shutdown
exit

!
! Trunk to Distribution Switch
!
interface GigabitEthernet0/4
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,60,70,80,90,99
 no shutdown

!
! Rapid PVST
!
spanning-tree mode rapid-pvst

!
! Secondary Root
!
spanning-tree vlan 1,10,20,30,40,50,60,70,80,90 root secondary

!
! Default Route
!
ip route 0.0.0.0 0.0.0.0 10.0.1.5

end
write memory

CORE1 (3560 Multilayer Switch)
enable
configure terminal

hostname CORE1

no ip domain-lookup
service password-encryption

enable secret Cisco123

banner motd #
AUTHORIZED USERS ONLY
#

ip domain-name enterprise.local

username admin privilege 15 secret Cisco123

crypto key generate rsa
1024

ip ssh version 2

line console 0
password cisco
login
logging synchronous
exit

line vty 0 15
login local
transport input ssh
exit

!
! Enable Layer 3 Routing
!
ip routing

!
! VLAN Creation
!
vlan 10
 name MANAGEMENT
exit

vlan 20
 name HR
exit

vlan 30
 name FINANCE
exit

vlan 40
 name SALES
exit

vlan 50
 name IT
exit

vlan 60
 name SERVER
exit

vlan 70
 name PRINTER
exit

vlan 80
 name GUEST_WIFI
exit

vlan 90
 name EMPLOYEE_WIFI
exit

vlan 99
 name NATIVE
exit

!
! SVI Interfaces
!

interface vlan 10
 ip address 192.168.10.1 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown
exit

interface vlan 20
 ip address 192.168.20.1 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown
exit

interface vlan 30
 ip address 192.168.30.1 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown
exit

interface vlan 40
 ip address 192.168.40.1 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown
exit

interface vlan 50
 ip address 192.168.50.1 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown
exit

interface vlan 60
 ip address 192.168.60.1 255.255.255.0
 no shutdown
exit

interface vlan 70
 ip address 192.168.70.1 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown
exit

interface vlan 80
 ip address 192.168.80.1 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown
exit

interface vlan 90
 ip address 192.168.90.1 255.255.255.0
 ip helper-address 192.168.60.10
 no shutdown
exit

!
! Routed Port to HQ Router
!
interface GigabitEthernet0/1
 no switchport
 ip address 10.0.1.2 255.255.255.252
 no shutdown
exit

!
! Trunk to CORE2
!
interface GigabitEthernet0/2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,60,70,80,90,99
 no shutdown
exit

!
! Trunk to Distribution Switch
!
interface GigabitEthernet0/3
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,60,70,80,90,99
 no shutdown
exit

interface GigabitEthernet0/4
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,60,70,80,90,99
 no shutdown
exit

!
! Rapid PVST
!
spanning-tree mode rapid-pvst

spanning-tree vlan 1,10,20,30,40,50,60,70,80,90 root primary

!
! Default Route
!
ip route 0.0.0.0 0.0.0.0 10.0.1.1

end

copy running-config startup-config

BRANCH ROUTER (2911)
enable
configure terminal

hostname BRANCH-R1

no ip domain-lookup

service password-encryption

enable secret Cisco123

banner motd #
AUTHORIZED USERS ONLY
#

ip domain-name enterprise.local

username admin privilege 15 secret Cisco123

crypto key generate rsa
1024

ip ssh version 2

line console 0
password cisco
login
logging synchronous
exit

line vty 0 15
login local
transport input ssh
exit

!
interface GigabitEthernet0/0
 description TO-HQ
 ip address 10.0.0.6 255.255.255.252
 no shutdown
exit

interface GigabitEthernet0/1
 description TO-BRANCH-L3
 ip address 10.0.2.1 255.255.255.252
 no shutdown
exit

ip route 0.0.0.0 0.0.0.0 10.0.0.5

ip route 192.168.110.0 255.255.255.0 10.0.2.2
ip route 192.168.120.0 255.255.255.0 10.0.2.2

end

copy running-config startup-config

HQ EDGE ROUTER (1941)
enable
configure terminal

hostname HQ-R1

no ip domain-lookup
service password-encryption

enable secret Cisco123

banner motd #
AUTHORIZED USERS ONLY
#

ip domain-name enterprise.local

username admin privilege 15 secret Cisco123

crypto key generate rsa
1024

ip ssh version 2

line console 0
password cisco
login
logging synchronous
exit

line vty 0 15
login local
transport input ssh
exit

!
interface GigabitEthernet0/0
 description TO-ISP
 ip address 10.0.0.2 255.255.255.252
 no shutdown
exit

interface GigabitEthernet0/1
 description TO-CORE1
 ip address 10.0.1.1 255.255.255.252
 no shutdown
exit

interface GigabitEthernet0/2
 description TO-BRANCH
 ip address 10.0.0.5 255.255.255.252
 no shutdown
exit

ip route 0.0.0.0 0.0.0.0 10.0.0.1

ip route 192.168.10.0 255.255.255.0 10.0.1.2
ip route 192.168.20.0 255.255.255.0 10.0.1.2
ip route 192.168.30.0 255.255.255.0 10.0.1.2
ip route 192.168.40.0 255.255.255.0 10.0.1.2
ip route 192.168.50.0 255.255.255.0 10.0.1.2
ip route 192.168.60.0 255.255.255.0 10.0.1.2
ip route 192.168.70.0 255.255.255.0 10.0.1.2
ip route 192.168.80.0 255.255.255.0 10.0.1.2
ip route 192.168.90.0 255.255.255.0 10.0.1.2

ip route 192.168.100.0 255.255.255.0 10.0.0.6

end
copy running-config startup-config


OLUME 1 – ISP Router (ISR4331)
enable
configure terminal

hostname ISP

no ip domain-lookup
service password-encryption

enable secret Cisco123

banner motd #
UNAUTHORIZED ACCESS PROHIBITED
#

ip domain-name enterprise.local

username admin privilege 15 secret Cisco123

crypto key generate rsa
1024

ip ssh version 2

line console 0
password cisco
login
logging synchronous
exec-timeout 10 0
exit

line vty 0 15
login local
transport input ssh
exec-timeout 10 0
exit

!
interface GigabitEthernet0/0/0
 description TO-INTERNET
 ip address 200.1.1.1 255.255.255.252
 no shutdown
exit

interface GigabitEthernet0/0/1
 description TO-HQ-ROUTER
 ip address 10.0.0.1 255.255.255.252
 no shutdown
exit

ip route 192.168.0.0 255.255.0.0 10.0.0.2

end
copy running-config startup-config

DIST1 (3560 Layer 3 Switch)

enable
configure terminal

hostname DIST1

no ip domain-lookup

service password-encryption

enable secret Cisco123

banner motd #
AUTHORIZED USERS ONLY
#

ip domain-name enterprise.local

username admin privilege 15 secret Cisco123

crypto key generate rsa
1024

ip ssh version 2

line console 0
 password cisco
 login
 logging synchronous
exit

line vty 0 15
 login local
 transport input ssh
exit

!
! Enable Layer 3 Routing
!
ip routing

!
! VLAN Creation
!
vlan 10
 name MANAGEMENT

vlan 20
 name HR

vlan 30
 name FINANCE

vlan 40
 name SALES

vlan 99
 name NATIVE

!
! Trunk to CORE1
!
interface GigabitEthernet0/1
 description Uplink-CORE1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,99
 no shutdown

!
! Trunk to CORE2
!
interface GigabitEthernet0/2
 description Uplink-CORE2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,99
 no shutdown

!
! HR Access Switch
!
interface FastEthernet0/1
 description HR-SW
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,99
 no shutdown

!
! Finance Access Switch
!
interface FastEthernet0/2
 description FINANCE-SW
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,30,99
 no shutdown

!
! Sales Access Switch
!
interface FastEthernet0/3
 description SALES-SW
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,40,99
 no shutdown

!
! Management Interface
!
interface vlan10
 ip address 192.168.10.11 255.255.255.0
 no shutdown

!
! Default Gateway
!
ip default-gateway 192.168.10.1

!
! Rapid PVST
!
spanning-tree mode rapid-pvst

spanning-tree portfast default

spanning-tree bpduguard default

end

copy running-config startup-config


enable
configure terminal

hostname DIST1

no ip domain-lookup

service password-encryption

enable secret Cisco123

banner motd #
AUTHORIZED USERS ONLY
#

ip domain-name enterprise.local

username admin privilege 15 secret Cisco123

crypto key generate rsa
1024

ip ssh version 2

line console 0
 password cisco
 login
 logging synchronous
exit

line vty 0 15
 login local
 transport input ssh
exit

!
! Enable Layer 3 Routing
!
ip routing

!
! VLAN Creation
!
vlan 10
 name MANAGEMENT

vlan 20
 name HR

vlan 30
 name FINANCE

vlan 40
 name SALES

vlan 99
 name NATIVE

!
! Trunk to CORE1
!
interface GigabitEthernet0/1
 description Uplink-CORE1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,99
 no shutdown

!
! Trunk to CORE2
!
interface GigabitEthernet0/2
 description Uplink-CORE2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,99
 no shutdown

!
! HR Access Switch
!
interface FastEthernet0/1
 description HR-SW
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,99
 no shutdown

!
! Finance Access Switch
!
interface FastEthernet0/2
 description FINANCE-SW
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,30,99
 no shutdown

!
! Sales Access Switch
!
interface FastEthernet0/3
 description SALES-SW
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,40,99
 no shutdown

!
! Management Interface
!
interface vlan10
 ip address 192.168.10.11 255.255.255.0
 no shutdown

!
! Default Gateway
!
ip default-gateway 192.168.10.1

!
! Rapid PVST
!
spanning-tree mode rapid-pvst

spanning-tree portfast default

spanning-tree bpduguard default

end

copy running-config startup-config


DIST2 (Cisco 3560 Layer 3 Switch)

enable
configure terminal

hostname DIST2

no ip domain-lookup
service password-encryption

enable secret Cisco123

banner motd #
AUTHORIZED USERS ONLY
#

ip domain-name enterprise.local

username admin privilege 15 secret Cisco123

crypto key generate rsa
1024

ip ssh version 2

line console 0
 password cisco
 login
 logging synchronous
exit

line vty 0 15
 login local
 transport input ssh
exit

!
! Enable Layer 3 Routing
!
ip routing

!
! VLAN Creation
!
vlan 10
 name MANAGEMENT

vlan 50
 name IT

vlan 60
 name SERVER

vlan 70
 name PRINTER

vlan 80
 name GUEST_WIFI

vlan 90
 name EMPLOYEE_WIFI

vlan 99
 name NATIVE

!
!=========================
! Uplink to CORE1
!=========================
interface GigabitEthernet0/1
 description Uplink-CORE1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,50,60,70,80,90,99
 no shutdown

!
!=========================
! Uplink to CORE2
!=========================
interface GigabitEthernet0/2
 description Uplink-CORE2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,50,60,70,80,90,99
 no shutdown

!
!=========================
! IT Access Switch
!=========================
interface FastEthernet0/1
 description IT-SW
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,50,99
 no shutdown

!
!=========================
! Server Switch
!=========================
interface FastEthernet0/2
 description SERVER-SW
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,60,99
 no shutdown

!
!=========================
! Wireless Switch
!=========================
interface FastEthernet0/3
 description WIRELESS-SW
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,80,90,99
 no shutdown

!
!=========================
! Printer Switch
!=========================
interface FastEthernet0/4
 description PRINTER-SW
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,70,99
 no shutdown

!
!=========================
! Management SVI
!=========================
interface vlan10
 ip address 192.168.10.12 255.255.255.0
 no shutdown

!
! Default Gateway
!
ip default-gateway 192.168.10.1

!
!=========================
! Rapid PVST
!=========================
spanning-tree mode rapid-pvst

spanning-tree portfast default

spanning-tree bpduguard default

!
!=========================
! DHCP Snooping
!=========================
ip dhcp snooping

ip dhcp snooping vlan 10,50,60,70,80,90

interface GigabitEthernet0/1
 ip dhcp snooping trust

interface GigabitEthernet0/2
 ip dhcp snooping trust

!
!=========================
! Dynamic ARP Inspection
!=========================
ip arp inspection vlan 10,50,60,70,80,90

interface GigabitEthernet0/1
 ip arp inspection trust

interface GigabitEthernet0/2
 ip arp inspection trust

!
!=========================
! Errdisable Recovery
!=========================
errdisable recovery cause bpduguard

end

copy running-config startup-config

HR-SW (2960)

enable
configure terminal

hostname HR-SW

no ip domain-lookup

service password-encryption

enable secret Cisco123

banner motd #
AUTHORIZED USERS ONLY
#

ip domain-name enterprise.local

username admin privilege 15 secret Cisco123

crypto key generate rsa
1024

ip ssh version 2

line console 0
password cisco
login
logging synchronous
exec-timeout 10 0
exit

line vty 0 15
login local
transport input ssh
exec-timeout 10 0
exit

!
!==============================
! VLANs
!==============================
vlan 10
 name MANAGEMENT

vlan 20
 name HR

vlan 99
 name NATIVE

!
!==============================
! Management Interface
!==============================
interface vlan10
 ip address 192.168.10.21 255.255.255.0
 no shutdown

ip default-gateway 192.168.10.1

!
!==============================
! Uplink to DIST1
!==============================
interface GigabitEthernet0/1
 description Uplink-to-DIST1
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,99
 spanning-tree link-type point-to-point
 no shutdown

!
!==============================
! HR PCs
!==============================
interface range FastEthernet0/1-20

 description HR-PCs

 switchport mode access

 switchport access vlan 20

 spanning-tree portfast

 spanning-tree bpduguard enable

 switchport port-security

 switchport port-security maximum 2

 switchport port-security mac-address sticky

 switchport port-security violation restrict

 storm-control broadcast level 5

 storm-control multicast level 5

 no shutdown

exit

!
!==============================
! HR Printer
!==============================
interface FastEthernet0/21

 description HR-Printer

 switchport mode access

 switchport access vlan 20

 spanning-tree portfast

 spanning-tree bpduguard enable

 switchport port-security

 switchport port-security maximum 1

 switchport port-security mac-address sticky

 switchport port-security violation restrict

 no shutdown

exit

!
!==============================
! Shutdown Unused Ports
!==============================
interface range FastEthernet0/22-24

 shutdown

 description UNUSED

exit

!
!==============================
! Rapid PVST
!==============================
spanning-tree mode rapid-pvst

spanning-tree portfast default

spanning-tree bpduguard default

!
!==============================
! DHCP Snooping
!==============================
ip dhcp snooping

ip dhcp snooping vlan 10,20

interface GigabitEthernet0/1
 ip dhcp snooping trust

!
!==============================
! Dynamic ARP Inspection
!==============================
ip arp inspection vlan 10,20

interface GigabitEthernet0/1
 ip arp inspection trust

!
!==============================
! Errdisable Recovery
!==============================
errdisable recovery cause bpduguard

end

copy running-config startup-config

Finance Access Switch (FIN-SW)

enable
configure terminal

hostname FIN-SW

no ip domain-lookup
service password-encryption
enable secret Cisco123

banner motd #
AUTHORIZED USERS ONLY
#

ip domain-name enterprise.local

username admin privilege 15 secret Cisco123

crypto key generate rsa
1024

ip ssh version 2

line console 0
password cisco
login
logging synchronous
exit

line vty 0 15
login local
transport input ssh
exit

vlan 10
 name MANAGEMENT

vlan 30
 name FINANCE

vlan 99
 name NATIVE

interface vlan10
 ip address 192.168.10.22 255.255.255.0
 no shutdown

ip default-gateway 192.168.10.1

interface GigabitEthernet0/1
 description Uplink-DIST1
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,30,99
 no shutdown

interface range FastEthernet0/1-20
 description Finance-PCs
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
 spanning-tree bpduguard enable
 switchport port-security
 switchport port-security maximum 2
 switchport port-security mac-address sticky
 switchport port-security violation restrict
 no shutdown

interface FastEthernet0/21
 description Finance-Printer
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky
 no shutdown

interface range FastEthernet0/22-24
 shutdown

spanning-tree mode rapid-pvst

ip dhcp snooping
ip dhcp snooping vlan 10,30

interface GigabitEthernet0/1
 ip dhcp snooping trust

ip arp inspection vlan 10,30

interface GigabitEthernet0/1
 ip arp inspection trust

end
write memory


PART 8 – SERVER ACCESS SWITCH (SERVER-SW)


enable
configure terminal

hostname SERVER-SW

no ip domain-lookup
service password-encryption

enable secret Cisco123

ip domain-name enterprise.local

username admin privilege 15 secret Cisco123

crypto key generate rsa
1024

ip ssh version 2

vlan 10
 name MANAGEMENT

vlan 60
 name SERVER

vlan 99
 name NATIVE

interface vlan10
 ip address 192.168.10.25 255.255.255.0
 no shutdown

ip default-gateway 192.168.10.1

!
! Uplink
!
interface GigabitEthernet0/1
 description Uplink-to-DIST2
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,60,99
 no shutdown

!
! Server Ports
!
interface range FastEthernet0/1-12
 description Server Ports
 switchport mode access
 switchport access vlan 60
 spanning-tree portfast
 spanning-tree bpduguard enable
 no shutdown

!
! Shutdown unused ports
!
interface range FastEthernet0/13-24
 shutdown

spanning-tree mode rapid-pvst

end

copy running-config startup-config


PART 9 – PRINTER SWITCH (PRINTER-SW)

enable

configure terminal

hostname PRINTER-SW

no ip domain-lookup

enable secret Cisco123

vlan 10
 name MANAGEMENT

vlan 70
 name PRINTER

vlan 99
 name NATIVE

interface vlan10

 ip address 192.168.10.26 255.255.255.0

 no shutdown

ip default-gateway 192.168.10.1

interface GigabitEthernet0/1

 switchport mode trunk

 switchport trunk native vlan 99

 switchport trunk allowed vlan 10,70,99

 no shutdown

interface range FastEthernet0/1-24

 switchport mode access

 switchport access vlan 70

 spanning-tree portfast

 spanning-tree bpduguard enable

 no shutdown

end

write memory


PART 10 – WIRELESS SWITCH

enable

configure terminal

hostname WIRELESS-SW

no ip domain-lookup

enable secret Cisco123

vlan 10
 name MANAGEMENT

vlan 80
 name GUEST

vlan 90
 name EMPLOYEE

vlan 99
 name NATIVE

interface vlan10

 ip address 192.168.10.27 255.255.255.0

 no shutdown

ip default-gateway 192.168.10.1

!
! Uplink
!
interface GigabitEthernet0/1

 switchport mode trunk

 switchport trunk native vlan 99

 switchport trunk allowed vlan 10,80,90,99

 no shutdown

!
! Wireless AP
!
interface FastEthernet0/1

 switchport mode trunk

 switchport trunk native vlan 99

 switchport trunk allowed vlan 80,90,99

 no shutdown

end

copy running-config startup-config

PART 11 – BRANCH ACCESS SWITC

enable

configure terminal

hostname BRANCH-SW

no ip domain-lookup

enable secret Cisco123

vlan 110
 name BRANCH_USERS

vlan 120
 name BRANCH_IT

vlan 199
 name NATIVE

interface vlan110

 ip address 192.168.110.2 255.255.255.0

 no shutdown

ip default-gateway 192.168.110.1

interface GigabitEthernet0/1

 switchport mode trunk

 switchport trunk native vlan 199

 switchport trunk allowed vlan 110,120,199

 no shutdown

interface range FastEthernet0/1-24

 switchport mode access

 switchport access vlan110

 spanning-tree portfast

 spanning-tree bpduguard enable

 no shutdown

end

write memory



PART 12 – DHCP SERVER CONFIGURATION (Packet Tracer Server)

This is configured on the Server-PT, not by CLI.

Desktop → IP Configuration
Setting	Value
IP Address	192.168.60.10
Subnet Mask	255.255.255.0
Default Gateway	192.168.60.1
DNS	192.168.60.10


Services → DHCP → ON

Create these DHCP pools:

Pool 1
Pool Name: Management

Gateway: 192.168.10.1

DNS: 192.168.60.10

Start IP: 192.168.10.100

Mask: 255.255.255.0

Maximum Users: 100
Pool 2
Pool Name: HR

Gateway: 192.168.20.1

DNS: 192.168.60.10

Start IP: 192.168.20.100

Mask: 255.255.255.0

Maximum Users: 100
Pool 3
Finance

Gateway 192.168.30.1

Start 192.168.30.100
Pool 4
Sales

Gateway 192.168.40.1

Start 192.168.40.100
Pool 5
IT

Gateway 192.168.50.1

Start 192.168.50.100
Pool 6
Printers

Gateway 192.168.70.1

Start 192.168.70.100
Pool 7
Guest WiFi

Gateway 192.168.80.1

Start 192.168.80.100
Pool 8
Employee WiFi

Gateway 192.168.90.1

Start 192.168.90.100



Configure DHCP Relay

On every Layer 3 VLAN interface (SVI) except VLAN 60, configure:

interface vlan20
 ip helper-address 192.168.60.10

interface vlan30
 ip helper-address 192.168.60.10

interface vlan40
 ip helper-address 192.168.60.10

interface vlan50
 ip helper-address 192.168.60.10

interface vlan70
 ip helper-address 192.168.60.10

interface vlan80
 ip helper-address 192.168.60.10

interface vlan90
 ip helper-address 192.168.60.10




PART 13 – Wireless Access Point Configuration

Assume:

Employee SSID → VLAN 90
Guest SSID → VLAN 80
Access Point
SSID: Enterprise-Employee

Security:
WPA2-PSK

Password:
Cisco@12345

VLAN:
90

Guest

SSID:
Enterprise-Guest

Security:
WPA2-PSK

Password:
Guest@123

VLAN:
80

Switch Port

interface FastEthernet0/1

description Wireless AP

switchport mode trunk

switchport trunk native vlan 99

switchport trunk allowed vlan 80,90,99

no shutdown
PART 14 – IPv6 Configuration

Enable IPv6 on every Router

configure terminal

ipv6 unicast-routing
CORE1 IPv6
interface vlan10

ipv6 address 2001:DB8:10::1/64

no shutdown

interface vlan20

ipv6 address 2001:DB8:20::1/64

no shutdown

interface vlan30

ipv6 address 2001:DB8:30::1/64

no shutdown

interface vlan40

ipv6 address 2001:DB8:40::1/64

no shutdown

interface vlan50

ipv6 address 2001:DB8:50::1/64

no shutdown

interface vlan60

ipv6 address 2001:DB8:60::1/64

no shutdown

interface vlan70

ipv6 address 2001:DB8:70::1/64

no shutdown

interface vlan80

ipv6 address 2001:DB8:80::1/64

no shutdown

interface vlan90

ipv6 address 2001:DB8:90::1/64

no shutdown
SLAAC
interface vlan20

ipv6 address 2001:DB8:20::1/64

ipv6 nd other-config-flag

no shutdown

Clients automatically receive

IPv6 Address
Default Gateway
Stateless DHCPv6
ipv6 dhcp pool HR

dns-server 2001:DB8:60::10

domain-name enterprise.local

Apply

interface vlan20

ipv6 dhcp server HR

ipv6 nd other-config-flag
Stateful DHCPv6

Create Pool

ipv6 dhcp pool SALES

address prefix 2001:DB8:40::/64

dns-server 2001:DB8:60::10

domain-name enterprise.local

Interface

interface vlan40

ipv6 dhcp server SALES

ipv6 nd managed-config-flag

Now DHCP Server gives

IPv6 Address
DNS
Domain Name
Static Routes IPv6

HQ Router

ipv6 route ::/0 2001:DB8:1::1

Branch Router

ipv6 route ::/0 2001:DB8:2::1
PART 15 – Final Verification
Routing
show ip route

show ipv6 route

show ip interface brief

show ipv6 interface brief
VLAN
show vlan brief

show interfaces trunk
STP
show spanning-tree

show spanning-tree root
EtherChannel
show etherchannel summary

show etherchannel port-channel
DHCP
show ip dhcp binding

show ip dhcp pool

show ip dhcp snooping

show ip helper-address
Security
show port-security

show port-security interface fa0/1

show ip arp inspection

show ip source binding
SSH
show ip ssh

show users
Interfaces
show interfaces status

show interfaces description

show cdp neighbors

show mac address-table
PART 16 – Final Testing

From every PC:

ipconfig

Should receive:

IP Address ✅
Gateway ✅
DNS ✅

Ping Gateway

ping 192.168.20.1

Ping Server

ping 192.168.60.10

Ping Another VLAN

ping 192.168.40.100

Ping Branch

ping 192.168.110.100

Traceroute

tracert 192.168.110.100

IPv6

ping 2001:DB8:20::1

ping 2001:DB8:40::100



CORE-SW0 (Cisco 3560 Multilayer Switch)


enable
configure terminal

hostname CORE-SW0

no ip domain-lookup

service password-encryption

enable secret Cisco123

banner motd #
AUTHORIZED USERS ONLY
#

ip domain-name enterprise.local

username admin privilege 15 secret Cisco123

crypto key generate rsa
1024

ip ssh version 2

line console 0
 password cisco
 login
 logging synchronous
 exec-timeout 10 0
exit

line vty 0 15
 login local
 transport input ssh
 exec-timeout 10 0
exit

!
! Enable Layer-3 Routing
!
ip routing

!
! VLANs
!
vlan 10
 name MANAGEMENT

vlan 20
 name HR

vlan 30
 name FINANCE

vlan 40
 name SALES

vlan 50
 name IT

vlan 60
 name SERVER

vlan 70
 name PRINTER

vlan 80
 name GUEST_WIFI

vlan 90
 name EMPLOYEE_WIFI

vlan 99
 name NATIVE

!
!===========================
! Management Interface
!===========================
interface vlan10
 ip address 192.168.10.3 255.255.255.0
 no shutdown

!
!===========================
! Routed Link to HQ Router
!===========================
interface GigabitEthernet0/1
 description Link-to-HQ-Router
 no switchport
 ip address 10.0.3.2 255.255.255.252
 no shutdown

!
!===========================
! Trunk to CORE1
!===========================
interface GigabitEthernet0/2
 description Link-to-CORE1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,60,70,80,90,99
 no shutdown

!
!===========================
! Trunk to CORE2
!===========================
interface GigabitEthernet0/3
 description Link-to-CORE2
 switchport trunk encapsulation dot1q
 switchport exitmode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,60,70,80,90,99
 no shutdown

!
!===========================
! Trunk to Distribution
!===========================
interface GigabitEthernet0/4
 description Link-to-DIST
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,60,70,80,90,99
 no shutdown

!
!===========================
! Rapid PVST
!===========================
spanning-tree mode rapid-pvst

spanning-tree vlan 1,10,20,30,40,50,60,70,80,90 priority 8192

!
!===========================
! DHCP Relay
!===========================
interface vlan20
 ip helper-address 192.168.60.10

interface vlan30
 ip helper-address 192.168.60.10

interface vlan40
 ip helper-address 192.168.60.10

interface vlan50
 ip helper-address 192.168.60.10

interface vlan70
 ip helper-address 192.168.60.10

interface vlan80
 ip helper-address 192.168.60.10

interface vlan90
 ip helper-address 192.168.60.10

!
!===========================
! Default Route
!===========================
ip route 0.0.0.0 0.0.0.0 10.0.3.1

!
!===========================
! DHCP Snooping
!===========================
ip dhcp snooping

ip dhcp snooping vlan 10,20,30,40,50,60,70,80,90

interface GigabitEthernet0/1
 ip dhcp snooping trust

interface GigabitEthernet0/2
 ip dhcp snooping trust

interface GigabitEthernet0/3
 ip dhcp snooping trust

!
!===========================
! Dynamic ARP Inspection
!===========================
ip arp inspection vlan 10,20,30,40,50,60,70,80,90

interface GigabitEthernet0/1
 ip arp inspection trust

interface GigabitEthernet0/2
 ip arp inspection trust

interface GigabitEthernet0/3
 ip arp inspection trust

end

copy running-config startup-config
