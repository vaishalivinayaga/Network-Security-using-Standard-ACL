# Network-Security-using-Standard-ACL


In our project, we are going to implement network security using standard ACL.
The main of our project is to ensure network security by not allowing any unauthorized users to access our network. In the implementation phase, we tend to block the malicious host who is trying to access the network by any means. We have also implemented the remove facility of malicious user by not letting them participate in the main network.
Access Control Lists (ACL) is a group of sequential statements that define whether packets are accepted or rejected coming into an interface or leaving an interface. 
ACL statements operate in sequential, logical order. If a condition match is true the packet is permitted or denied and the rest of Access Control List statements are not checked. If all the Access Control List statements are unmatched an implicit “deny any” statement is placed at the end of the list by default. Access Control List 
evaluates packets from the top down. Once there is an access list statement match, the packet skips the rest of the statements. If a condition match is true, the packet is permitted or denied.
We are using Standard ACL for the basic implementation of our project. Standard Access Control Lists are the oldest type of Access Control List. Standard IP Access 
Lists are used to permit or deny traffic only based on source IP address of IP datagram packets and it can be created by using the “access-list” IOS command.


Router0 Configuration:
Router>enable
Router#
Router#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#interface Serial0/0/0
Router(config-if)#ip address 10.0.0.1 255.255.255.252
Router(config-if)#clock rate 128000
Router(config-if)#no shutdown
%LINK-5-CHANGED: Interface Serial0/0/0, changed state to down
Router(config-if)#
Router(config-if)#exit
Router(config)#interface fastEthernet 0/0
Router(config-if)#ip address 192.168.10.1 255.255.255.0
Router(config-if)#no shutdown
Router(config-if)#
%LINK-5-CHANGED: Interface fastEthernet0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface fastEthernet0/0, changed 
state to
up
Router(config-if)#exit
Router(config)#
Router(config)#ip route 192.168.20.0 255.255.255.0 10.0.0.2
Router(config)#ip route 10.0.0.4 255.255.255.252 10.0.0.2
Router(config)#ip route 192.168.30.0 255.255.255.0 10.0.0.2
Router(config)#exit
Router#
Router#copy running-config start up-config 
Destination filename [startup-config]?
Building configuration…
[OK]
Router#exit



Router1 Configuration:
Router>enable
Router#
Router#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#interface Serial0/1/0
Router(config-if)#ip address 10.0.0.2 255.255.255.252
Router(config-if)#no shutdown
Router(config-if)#
%LINK-5-CHANGED: Interface Serial0/1/0, changed state to up
Router(config-if)# interface Serial0/0/0
Router(config-if)#ip address 10.0.0.5 255.255.255.252
Router(config-if)#clock rate 72000
Router(config-if)#no shutdown
Router(config-if)#
%LINK-5-CHANGED: Interface Serial0/0/0, changed state to up
Router(config-if)# interface fastEthernet 
%LINK-5-CHANGED: Interface Serial0/0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Serial0/0/0, changed state 
to
up
Router(config-if)#interface fastEthernet 0/0
Router(config-if)#ip address 192.168.20.1 255.255.255.0
Router(config-if)#no shutdown
Router(config-if)#
%LINK-5-CHANGED: Interface fastEthernet0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface fastEthernet0/0, changed 
state to
up
Router(config-if)#exit
Router(config)#
Router(config)#ip route 192.168.10.0 255.255.255.0 10.0.0.1
Router(config)#ip route 192.168.30.0 255.255.255.0 10.0.0.6
Router(config)#exit
Router#
%SYS-5-CONFIG_I: Configured from console by console
Router#copy running-config start up-config 
Destination filename [startup-config]?
Building configuration…
[OK]





Router#exit
Router>en
Router#config t
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#access-list ?
<1-99> IP standard access list
<100-199> IP extended access list
Router(config)#access-list 1 ?
deny Specify packets to reject
permit Specify packets to forward
remark Access list entry comment
Router(config)#access-list 1 deny 192.168.10.0
Router(config)#access-list 1 ?
deny Specify packets to reject
permit Specify packets to forward
remark Access list entry comment
Router(config)#access-list 1 deny 192.168.10.0 ?
A.B.C.D Wildcard bits
<cr>
Router(config)#access-list 1 deny 192.168.10.0 0.0.0.255 ?
<cr>
Router(config)#access-list 1 deny 192.168.10.0 0.0.0.255 
Router(config)#access-list 1 permit ?
A.B.C.D Address to match
any Any source host
host A single host address
Router(config)#access-list 1 permit any
Router(config)#interface fastEthernet 0/0
Router(config-if)#ip access-group 1 ?
in inbound packets
out outbound packets
Router(config-if)#ip access-group 1 out
Router(config-if)#
Router(config-if)#exit
Router#show access-lists
Standard IP access list 1
10 deny host 192.168.10.0
20 deny 192.168.10.0 0.0.0.255
30 permit any



Router2 Configuration:-
Router>enable
Router#
Router#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#interface Serial0/0/0
Router(config-if)#ip address 10.0.0.6 255.255.255.252
Router(config-if)#no shutdown
Router(config-if)#interface fastEthernet 0/0
Router(config-if)#ip address 192.168.30.1 255.255.255.0
Router(config-if)#no shutdown
%LINK-5-CHANGED: Interface fastEthernet0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface fastEthernet0/0, changed 
state to
up
Router(config-if)#exit
Router(config)#ip route 192.168.20.0 255.255.255.0 10.0.0.5
Router(config)#ip route 10.0.0.0 255.255.255.252 10.0.0.5
Router(config)#ip route 192.168.10.0 255.255.255.0 10.0.0.5
Router(config)#exit
Router#
%SYS-5-CONFIG_I: Configured from console by console
Router#copy running-config start up-config 
Destination filename [startup-config]?
Building configuration…
[OK]
Router#exit
