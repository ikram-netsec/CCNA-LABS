CCNA-OSPF-Multi-Router-Lab

Router R1 Configuration
enable
configure terminal

hostname R1

interface GigabitEthernet0/0
 description Link to 11.0.0.0 Network
 ip address 11.0.0.1 255.0.0.0
 no shutdown

interface GigabitEthernet0/1
 description Link to 10.0.0.0 Network
 ip address 10.0.0.1 255.0.0.0
 no shutdown

interface GigabitEthernet0/2
 description Link to 12.0.0.0 Network
 ip address 12.0.0.1 255.0.0.0
 no shutdown

interface Serial0/2/0
 description Link to R2
 bandwidth 2000000
 ip address 13.0.0.1 255.255.255.0
 clock rate 2000000
 no shutdown

router ospf 1
 log-adjacency-changes
 network 10.0.0.0 0.255.255.255 area 1
 network 11.0.0.0 0.255.255.255 area 1
 network 12.0.0.0 0.255.255.255 area 1
 network 13.0.0.0 0.0.0.3 area 1

end
write memory


Router R2 Configuration

enable
configure terminal

hostname R2

interface GigabitEthernet0/0/0
 description Link to 14.0.0.0 Network
 ip address 14.0.0.1 255.0.0.0
 no shutdown

interface GigabitEthernet0/0/1
 description Link to 16.0.0.0 Network
 ip address 16.0.0.1 255.0.0.0
 no shutdown

interface Serial0/1/0
 description Link to R1
 ip address 13.0.0.2 255.0.0.0
 no shutdown

interface Serial0/1/1
 description Link to R3
 bandwidth 2000000
 ip address 15.0.0.1 255.0.0.0
 clock rate 2000000
 no shutdown

router ospf 1
 log-adjacency-changes
 network 13.0.0.0 0.255.255.255 area 1
 network 14.0.0.0 0.255.255.255 area 1
 network 15.0.0.0 0.255.255.255 area 1
 network 16.0.0.0 0.255.255.255 area 1
 network 13.0.0.0 0.0.0.3 area 1
 network 15.0.0.0 0.0.0.3 area 1

end
write memory



Router R3 Configuration


enable
configure terminal

hostname R3

interface GigabitEthernet0/0
 description Link to 17.0.0.0 Network
 ip address 17.0.0.1 255.0.0.0
 no shutdown

interface GigabitEthernet0/1
 description Link to 19.0.0.0 Network
 ip address 19.0.0.1 255.0.0.0
 no shutdown

interface GigabitEthernet0/2
 description Link to 18.0.0.0 Network
 ip address 18.0.0.1 255.0.0.0
 no shutdown

interface Serial0/1/0
 description Link to R2
 ip address 15.0.0.2 255.0.0.0
 no shutdown

router ospf 1
 log-adjacency-changes
 network 15.0.0.0 0.0.0.3 area 1
 network 17.0.0.0 0.255.255.255 area 1
 network 18.0.0.0 0.255.255.255 area 1
 network 19.0.0.0 0.255.255.255 area 1

end
write memory
