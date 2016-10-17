## Installation
```bash
sudo apt-get install syslinux-common
sudo apt-get install tftpd-hpa
```
## tftpd en mode verbeux
```
sudo nano /etc/default/tftpd-hpa

# /etc/default/tftpd-hpa
TFTP_USERNAME="tftp"
TFTP_DIRECTORY="/var/lib/tftpboot"
TFTP_ADDRESS="[::]:69"
TFTP_OPTIONS="--secure -v -v -v -v"
```
## Modification du fichier /etc/dhcp/dhcpd.conf
```
subnet 192.168.42.0 netmask 255.255.255.0 {
    next-server 192.168.42.1; 
    filename "pxelinux.0";
    range 192.168.42.10 192.168.42.50;
```
Redémarrer le service pour que les modifications soient prises en compte
```
sudo service isc-dhcp-server restart
```
Copie des fichiers pxelinux.0 et menu.c32
```
sudo cp /usr/lib/syslinux/pxelinux.0 /var/lib/tftpboot/
sudo cp /usr/lib/syslinux/menu.c32 /var/lib/tftpboot/
<<<<<<< HEAD
=======
```

Debian 8 (Jessie) Copie des fichiers pxelinux.0 et menu.c32
```
sudo cp /usr/lib/PXELINUX/pxelinux.0 /var/lib/tftpboot/
sudo cp /usr/lib/syslinux/modules/bios/menu.c32 /var/lib/tftpboot/
```

## Création du fichier /var/lib/tftpboot/pxelinux.cfg/default
```
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
>>>>>>> ff1551bab8aa23cbb55f1e706f69f25067c55164
```
Coté client

<<<<<<< HEAD
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

=======
![Vue du coté client](https://github.com/havresac/stage-debian-server/blob/master/img/client-pxe.png)
>>>>>>> ff1551bab8aa23cbb55f1e706f69f25067c55164
