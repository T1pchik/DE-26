- BR-SRV
```tcl
hostnamectl set-hostname br-srv.au-team.irpo
exec bash
mkdir /etc/net/ifaces/ens20

 vim /etc/net/ifaces/ens20/ipv4address
	192.168.3.10/28
 vim /etc/net/ifaces/ens20/ipv4route
	default via 192.168.3.1
vim /etc/resolv.conf 
	nameserver 8.8.8.8 
systemctl restart network
useradd remote_user -u 2026
passwd remote_user
P@ssw0rd 
P@ssw0rd 
gpasswd -a “remote_user” wheel
vim /etc/sudoers
	WHEEL_USERS ALL=(ALL:ALL) NOPASSWD: ALL
vim /etc/openssh/sshd_config
	Port 2026
	AllowUsers remote_user
	MaxAuthTries 2
	PasswordAuthentication yes
	Banner /etc/openssh/banner 
vim /etc/openssh/banner
ᅠ ᅠ`Authorized access only`
systemctl restart sshd
timedatectl set-timezone Asia/Yekaterinburg
```
