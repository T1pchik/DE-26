```tcl
tee /etc/111/testnginx1 > /dev/null << 'EOF'
server {
    listen 80;
    server_name web.au-team.irpo;
    
    location / {
        proxy_pass http://172.16.1.2:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

server {
    listen 80;
    server_name docker.au-team.irpo;
    
    location / {
        proxy_pass http://172.16.2.2:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
EOF
```

**ФИКС WEB**
```tcl
apt-get update
apt-get install -y apache2 php8.2 apache2-mod_php8.2 mariadb-server php8.2-{opcache,curl,gd,intl,mysqli,xml,xmlrpc,ldap,zip,soap,mbstring,json,xmlreader,fileinfo,sodium}
sleep 4
mount -o loop /dev/sr0
systemctl enable --now httpd2 mysqld
mysql_secure_installation

mariadb -u root -p
CREATE DATABASE webdb;
CREATE USER 'webc'@'localhost' IDENTIFIED BY 'P@ssw0rd';
GRANT ALL PRIVILEGES ON webdb.* TO 'webc'@'localhost';
FLUSH PRIVILEGES;
exit
iconv -f UTF-16LE -t UTF-8 /media/ALTLinux/web/dump.sql > /tmp/dump_utf8.sql
mariadb -u root -p webdb < /tmp/dump_utf8.sql
chmod 777 /var/www/html
cp /media/ALTLinux/web/index.php /var/www/html
cp /media/ALTLinux/web/logo.png /var/www/html
rm -f /var/www/html/index.html
chown apache2:apache2 /var/www/html
systemctl restart httpd2*

/var/www/html/index.php
$servername = "localhost";
$username = "webc";
$password = "P@ssw0rd";
$dbname = "webdb";
```
