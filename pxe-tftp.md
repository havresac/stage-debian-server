## Installation
```
sudo apt-get install syslinux-common
sudo apt-get install tftpd-hpa
```

## Modification du fichier /etc/dhcp/dhcpd.conf
```
subnet 192.168.42.0 netmask 255.255.255.0 {
    next-server 192.168.42.1; 
    filename "pxelinux.0";
    range 192.168.42.10 192.168.42.50;
```

Copie du fichier pxelinux.0
```
sudo cp /usr/lib/syslinux/pxelinux.0 /var/lib/tftpboot/
```

