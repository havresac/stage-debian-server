## Installation
```
sudo apt-get install syslinux-common
sudo apt-get install tftpd-hpa
```

next-server 10.72.8.1; 
filename "pxelinux.0"; 

## Modification du fichier /etc/dhcp/dhcpd.conf

subnet 192.168.42.0 netmask 255.255.255.0 {
**    next-server 192.168.42.1; 
    filename "pxelinux.0"; **
    range 192.168.42.10 192.168.42.50;

Copie du fichier pxelinux.0
```
sudo cp /usr/lib/syslinux/pxelinux.0 /var/lib/tftpboot/
sudo cp /usr/lib/syslinux/menu.c32 /var/lib/tftpboot/
```

## Création du fichier /var/lib/tftpboot/pxelinux.cfg/default


sudo mkdir /var/lib/tftpboot/pxelinux.cfg
sudo nano /var/lib/tftpboot/pxelinux.cfg/default


ALLOWOPTIONS 1
PROMPT 0
TIMEOUT 20
DEFAULT menu.c32

MENU TITLE PXE SIDSIC de la Sarthe
MENU AUTOBOOT Boot automatique dans # s

label  local
	MENU LABEL BOOT disque dur
	LOCALBOOT 0

