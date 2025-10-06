- HQ-CLI
```tcl
su -
toor
hostnamectl set-hostname hq-cli.au-team.irpo
mkdir /etc/net/ifaces/ens20
echo -e "DISABLED=no\nTYPE=eth\nBOOTPROTO=static\nCONFIG_IPv4=yes" > /etc/net/ifaces/ens20/options
systemctl restart network
timedatectl set-timezone Asia/Yekaterinburg
exec bash
```
