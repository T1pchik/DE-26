hostnamectl set-hostname isp;exec bash
mkdir /etc/net/ifaces/ens20
mkdir /etc/net/ifaces/ens21
mkdir /etc/net/ifaces/ens22
tee /etc/net/ifaces/ens20/options > /dev/null << EOF TYPE=eth BOOTPROTO=static DISABLED=no CONFIG_IPV4=yes EOF
---
