- BR-RTR
```tcl
en
conf t
hostname br-rtr 
ip domain-name au-team.irpo
interface int0
ip nat outside
ip address 172.16.2.2/28
ex
port te0
service-instance te0/int0
encapsulation untagged
ex
ex
interface int0
connect port te0 service-instance te0/int0
ex
interface int1
ip nat inside
ip address 192.168.3.1/28
ex
port te1
service-instance te1/int1
encapsulation untagged
ex
ex
interface int1
connect port te1 service-instance te1/int1
ex
ip route 0.0.0.0 0.0.0.0 172.16.2.1
ip name-server 8.8.8.8
ip nat pool NAT_POOL 192.168.3.1-192.168.3.254
ip nat source dynamic inside-to-outside pool NAT_POOL overload interface int0
int tunnel.0
ip address 172.16.0.2/30
ip mtu 1400
ip tunnel 172.16.2.2 172.16.1.2 mode gre 
ip ospf authentication-key ecorouter 
ex
router ospf 1
network 172.16.0.0/28 area 0
network 192.168.3.0/28 area 0
passive-interface default 
no passive-interface tunnel.0
area 0 authentication
ex
ntp timezone utc+5
username net_admin 
password P@ssw0rd 
role admin
end
wr mem
```
