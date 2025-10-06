- BR-SRV
```tcl
hostnamectl set-hostname br-srv.au-team.irpo
exec bash
mkdir /etc/net/ifaces/ens20
echo -e "DISABLED=no\nTYPE=eth\nBOOTPROTO=static\nCONFIG_IPv4=yes" > /etc/net/ifaces/ens20/options
echo -e "192.168.3.10/28" > /etc/net/ifaces/ens20/ipv4address
echo -e "default via 192.168.3.1" > /etc/net/ifaces/ens20/ipv4route
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
```
