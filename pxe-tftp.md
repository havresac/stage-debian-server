
## Installation

```
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
```

## Contenu du fichier default
```
# Interface visuelle
MENU TITLE PXE SIDSIC de la Sarthe
MENU AUTOBOOT Boot automatique dans # s

# Entrée pour booter à partir du disque local
label  local
    MENU LABEL BOOT disque dur
    LOCALBOOT 0

# Entrée du menu permettant de lancer depuis le serveur SystemRescuCD
LABEL SRCD
    MENU LABEL SystemRescueCD 4.8.3
    kernel sysrcd/rescue64
    append initrd=sysrcd/initram.igz netboot=http://192.168.42.1/sysrcd/sysrcd.dat setkmap=fr

# Entrée du menu permettant de lancer depuis le serveur Clonezilla
label Clonzilla-live
    MENU LABEL Clonezilla Live (Ramdisk)
    kernel clonezilla/live/vmlinuz
    append initrd=clonezilla/live/initrd.img boot=live union=overlay username=user config components quiet noswap edd=on nomodeset nodmraid locales=keyboard-layouts=ocs_live_run="ocs-live-general" ocs_live_extra_param="" ocs_live_batch=no net.iframes=0 nosplash noprompt fetch=tftp://192.168.42.1/clonezilla/live/filesystem.squashfs 

```
Coté client


![Vue du coté client](https://github.com/havresac/stage-debian-server/blob/master/img/client-pxe.png)


