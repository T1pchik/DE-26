- ISP
```tcl
hostnamectl set-hostname isp
mkdir /etc/net/ifaces/ens20
mkdir /etc/net/ifaces/ens21
mkdir /etc/net/ifaces/ens22
echo -e "DISABLED=no\nTYPE=eth\nBOOTPROTO=static\nCONFIG_IPv4=yes" > /etc/net/ifaces/ens20/options
```
