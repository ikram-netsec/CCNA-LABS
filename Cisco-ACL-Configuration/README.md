Cisco-ACL-Configuration

enable
configure terminal

! =========================
! ACL 101 - Internet Traffic
! =========================
access-list 101 remark BLOCK FTP FROM INTERNET TO ENTERPRISE WEB SERVER
access-list 101 deny tcp any host 192.168.1.70 eq ftp

access-list 101 remark BLOCK ICMP FROM INTERNET TO HQ LAN 1
access-list 101 deny icmp any 192.168.1.0 0.0.0.63

access-list 101 remark ALLOW ALL OTHER TRAFFIC
access-list 101 permit ip any any

interface s0/1/0
 description INTERNET CONNECTION - ACL 101 INBOUND
 ip access-group 101 in
exit


! =========================
! ACL 111 - HQ LAN 1 Access
! =========================
access-list 111 remark BLOCK HQ LAN 1 TO BRANCH SERVER
access-list 111 deny ip 192.168.1.0 0.0.0.63 host 192.168.2.45

access-list 111 remark ALLOW ALL OTHER TRAFFIC
access-list 111 permit ip any any

interface g0/0/0
 description HQ LAN 1 - ACL 111 INBOUND
 ip access-group 111 in
exit


! =========================
! VTY BLOCK - Standard ACL
! =========================
ip access-list standard vty_block
 remark ALLOW ONLY HQ LAN 2 TO ACCESS VTY
 permit 192.168.1.64 0.0.0.7
exit

line vty 0 4
 access-class vty_block in
exit

Branch Router

enable
configure terminal

! =================================
! branch_to_hq - Extended Named ACL
! =================================
ip access-list extended branch_to_hq

 remark BLOCK BRANCH LAN 1 TO HQ LAN 1
 deny ip 192.168.2.0 0.0.0.31 192.168.1.0 0.0.0.63

 remark BLOCK BRANCH LAN 2 TO HQ LAN 1
 deny ip 192.168.2.32 0.0.0.15 192.168.1.0 0.0.0.63

 remark ALLOW ALL OTHER TRAFFIC
 permit ip any any

exit

interface g0/0/0
 description BRANCH LAN 1 - ACL BRANCH_TO_HQ INBOUND
 ip access-group branch_to_hq in
exit

interface g0/0/1
 description BRANCH LAN 2 - ACL BRANCH_TO_HQ INBOUND
 ip access-group branch_to_hq in
exit

end
write memory



end
write memory
