- ISP
```tcl
hostnamectl set-hostname isp
exec bash
mkdir /etc/net/ifaces/ens20
mkdir /etc/net/ifaces/ens21
mkdir /etc/net/ifaces/ens22
echo -e "DISABLED=no\nTYPE=eth\nBOOTPROTO=dhcp\nCONFIG_IPv4=yes" > /etc/net/ifaces/ens20/options
echo -e "DISABLED=no\nTYPE=eth\nBOOTPROTO=static\nCONFIG_IPv4=yes" > /etc/net/ifaces/ens21/options
echo -e "DISABLED=no\nTYPE=eth\nBOOTPROTO=static\nCONFIG_IPv4=yes" > /etc/net/ifaces/ens22/options
echo -e "172.16.1.1/28" > /etc/net/ifaces/ens21/ipv4address
echo -e "172.16.2.1/28" > /etc/net/ifaces/ens22/ipv4address
echo "net.ipv4.ip_forward = 1" >> /etc/net/sysctl.conf
systemctl restart network
apt-get update && apt-get install iptables -y
apt-get reinstall tzdata
timedatectl set-timezone Asia/Yekaterinburg
iptables -t nat -A POSTROUTING -o ens20 -s 0/0 -j MASQUERADE
iptables-save > /etc/sysconfig/iptables
systemctl enable --now iptables
```
