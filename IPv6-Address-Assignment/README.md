# IPv6 Address Assignment Lab

This folder contains my CCNA IPv6 labs covering:
- SLAAC
- Stateless DHCPv6
- Stateful DHCPv6
- DHCPv6 Relay
- Router Advertisement (RA)
- Neighbor Discovery (ND)
========================================
R1 CONFIGURATION
========================================

enable
configure terminal
hostname R1
no ip domain lookup
enable secret class

line console 0
 password cisco
 login
exit

line vty 0 4
 password cisco
 login
exit

service password-encryption
banner motd # Authorized Users Only! #

ipv6 unicast-routing

ipv6 dhcp pool R1-STATELESS
 dns-server 2001:DB8:ACAD::254
 domain-name STATELESS.com
exit

ipv6 dhcp pool R2-STATEFUL
 address prefix 2001:DB8:ACAD:3:AAAA::/80
 dns-server 2001:DB8:ACAD::254
 domain-name STATEFUL.com
exit

interface GigabitEthernet0/0/0
 ipv6 address FE80::1 link-local
 ipv6 address 2001:DB8:ACAD:2::1/64
 ipv6 dhcp server R2-STATEFUL
 no shutdown
exit

interface GigabitEthernet0/0/1
 ipv6 address FE80::1 link-local
 ipv6 address 2001:DB8:ACAD:1::1/64
 ipv6 nd other-config-flag
 ipv6 dhcp server R1-STATELESS
 no shutdown
exit

ipv6 route ::/0 2001:DB8:ACAD:2::2

end
copy running-config startup-config

========================================
R2 CONFIGURATION
========================================

enable
configure terminal
hostname R2
no ip domain lookup
enable secret class

line console 0
 password cisco
 login
exit

line vty 0 4
 password cisco
 login
exit

service password-encryption
banner motd # Authorized Users Only! #

ipv6 unicast-routing

interface GigabitEthernet0/0/0
 ipv6 address FE80::2 link-local
 ipv6 address 2001:DB8:ACAD:2::2/64
 no shutdown
exit

interface GigabitEthernet0/0/1
 ipv6 address FE80::2 link-local
 ipv6 address 2001:DB8:ACAD:3::1/64
 ipv6 nd prefix 2001:DB8:ACAD:3::/64 2592000 604800 no-autoconfig
 ipv6 nd managed-config-flag
 ipv6 dhcp relay destination 2001:DB8:ACAD:2::1 GigabitEthernet0/0/0
 no shutdown
exit

ipv6 route ::/0 2001:DB8:ACAD:2::1

end
copy running-config startup-config

========================================
S1 CONFIGURATION
========================================

enable
configure terminal
hostname S1
no ip domain-lookup
enable secret class

line console 0
 password cisco
 login
exit

line vty 0 4
 password cisco
 login
exit

service password-encryption
banner motd # Authorized Users Only! #

interface range f0/1-4,f0/7-24,g0/1-2
 shutdown
exit

end
copy running-config startup-config

========================================
S2 CONFIGURATION
========================================

enable
configure terminal
hostname S2
no ip domain-lookup
enable secret class

line console 0
 password cisco
 login
exit

line vty 0 4
 password cisco
 login
exit

service password-encryption
banner motd # Authorized Users Only! #

interface range f0/1-4,f0/6-17,f0/19-24,g0/1-2
 shutdown
exit

end
copy running-config startup-config
