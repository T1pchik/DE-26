- HQ-SRV
```tcl
hostnamectl set-hostname hq-srv.au-team.irpo
exec bash
mkdir /etc/net/ifaces/ens20
echo -e "DISABLED=no\nTYPE=eth\nBOOTPROTO=static\nCONFIG_IPv4=yes" > /etc/net/ifaces/ens20/options
echo -e "192.168.1.10/27" > /etc/net/ifaces/ens20/ipv4address
echo -e "default via 192.168.1.1" > /etc/net/ifaces/ens20/ipv4route
echo -e "nameserver 8.8.8.8 " > /etc/resolv.conf
systemctl restart network
useradd remote_user -u 2026
echo -e "P@ssw0rd\nP@ssw0rd" | passwd remote_user
gpasswd -a “remote_user” wheel
sed -i '/WHEEL_USERS.*ALL.*NOPASSWD.*ALL/s/^#//' /etc/sudoers
echo -e "Port 2026\nAllowUsers remote_user\nMaxAuthTries\nPasswordAuthentication yes\nBanner /etc/openssh/banner " > /etc/openssh/sshd_config
echo -e "Authorized access only" > /etc/openssh/banner
systemctl restart sshd
timedatectl set-timezone Asia/Yekaterinburg 
apt-get update && apt-get install dnsmasq –y
systemctl enable --now dnsmasq
echo -e "no-resolv\ndomain=au-team.irpo\nserver=8.8.8.8\ninterface=*\naddress=/hq-rtr.au-team.irpo/192.168.1.1\nptr-record=1.1.168.192.in-addr.arpa,hq-rtr.au-team.irpo\naddress=/hq-srv.au-team.irpo/192.168.1.10\nptr-record=10.1.168.192.in-addr.arpa,hq-srv.au-team.irpo\naddress=/hq-cli.au-team.irpo/192.168.2.10\nptr-record=10.2.168.192.in-addr.arpa,hq-cli.au-team.irpo\naddress=/br-rtr.au-team.irpo/192.168.3.1\naddress=/br-srv.au-team.irpo/192.168.3.10\naddress=/docker.au-team.irpo/172.16.1.1\naddress=/web.au-team.irpo/172.16.2.1" > /etc/dnsmasq.conf
echo -e "192.168.1.1  hq-rtr.au-team.irpo" > /etc/hosts
systemctl restart dnsmasq
```
