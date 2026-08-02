Completed a CCNA Switch Security Lab featuring VLANs, Port Security, DHCP Snooping, Dynamic ARP Inspection (DAI), BPDU Guard, Root Guard, Storm Control, SSH, and Router-on-a-Stick with DHCP. This hands-on lab enhanced my practical skills in securing Cisco switched networks.
Below is a complete CCNA Switch Security CLI configuration for a Cisco 2960 switch. You can paste it into Packet Tracer (adjust interface numbers if your switch model differs).
enable
configure terminal

!========================
! BASIC CONFIGURATION
!========================
hostname S1
no ip domain-lookup
enable secret class123
service password-encryption

banner motd #
*****************************************
* Unauthorized Access is Prohibited!    *
*****************************************
#

!========================
! VLAN CONFIGURATION
!========================
vlan 10
 name HR

vlan 20
 name Finance

vlan 30
 name IT

vlan 40
 name Guest

vlan 99
 name Management

vlan 999
 name BLACKHOLE

!========================
! ACCESS PORTS
!========================
interface fa0/1
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 spanning-tree bpduguard enable

interface fa0/2
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
 spanning-tree bpduguard enable

interface fa0/3
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
 spanning-tree bpduguard enable

interface fa0/4
 switchport mode access
 switchport access vlan 40
 spanning-tree portfast
 spanning-tree bpduguard enable

!========================
! PORT SECURITY
!========================
interface range fa0/1 - 4
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation restrict
 switchport port-security mac-address sticky

!========================
! UPLINK TO ROUTER
!========================
interface g0/1
 switchport mode trunk
 ip dhcp snooping trust
 ip arp inspection trust

!========================
! DHCP SNOOPING
!========================
ip dhcp snooping
ip dhcp snooping vlan 10,20,30,40

!========================
! DYNAMIC ARP INSPECTION
!========================
ip arp inspection vlan 10,20,30,40

!========================
! ROOT GUARD
!========================
interface fa0/24
 spanning-tree guard root

!========================
! STORM CONTROL
!========================
interface range fa0/1 - 4
 storm-control broadcast level 10.00
 storm-control action shutdown

!========================
! UNUSED PORTS
!========================
interface range fa0/5 - 23
 switchport mode access
 switchport access vlan 999
 shutdown

!========================
! SSH CONFIGURATION
!========================
ip domain-name ccna.local

username admin secret Cisco123

crypto key generate rsa modulus 2048

ip ssh version 2

line vty 0 15
 login local
 transport input ssh

!========================
! SAVE CONFIGURATION
!========================
end
copy running-config startup-config
Assuming:

R1 is the DHCP server.
S1 Gi0/1 is connected to R1 G0/0 as a trunk.
VLANs: 10, 20, 30, 40.
Router-on-a-Stick is used.

Use the following R1 configuration.
enable
configure terminal

!========================
! BASIC CONFIGURATION
!========================
hostname R1
no ip domain-lookup
enable secret class123
service password-encryption

banner motd #
Authorized Access Only!
#

!========================
! ENABLE INTERFACES
!========================
interface g0/0
 no shutdown

!========================
! VLAN 10
!========================
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

!========================
! VLAN 20
!========================
interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0

!========================
! VLAN 30
!========================
interface g0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0

!========================
! VLAN 40
!========================
interface g0/0.40
 encapsulation dot1Q 40
 ip address 192.168.40.1 255.255.255.0

!========================
! DHCP EXCLUDED ADDRESSES
!========================
ip dhcp excluded-address 192.168.10.1 192.168.10.20
ip dhcp excluded-address 192.168.20.1 192.168.20.20
ip dhcp excluded-address 192.168.30.1 192.168.30.20
ip dhcp excluded-address 192.168.40.1 192.168.40.20

!========================
! DHCP POOL VLAN10
!========================
ip dhcp pool VLAN10
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 8.8.8.8

!========================
! DHCP POOL VLAN20
!========================
ip dhcp pool VLAN20
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1
 dns-server 8.8.8.8

!========================
! DHCP POOL VLAN30
!========================
ip dhcp pool VLAN30
 network 192.168.30.0 255.255.255.0
 default-router 192.168.30.1
 dns-server 8.8.8.8

!========================
! DHCP POOL VLAN40
!========================
ip dhcp pool VLAN40
 network 192.168.40.0 255.255.255.0
 default-router 192.168.40.1
 dns-server 8.8.8.8

end
copy running-config startup-config
Verify

On the router:
show ip interface brief
show ip dhcp binding
show ip dhcp pool
show running-config
On the switch:
show interfaces trunk
show vlan brief
show ip dhcp snooping
show ip arp inspection

