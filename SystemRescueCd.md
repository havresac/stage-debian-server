## Installer un serveur web léger
sudo apt-get install lighttpd

Puis tester le bon fonctionnement dans un navigateur

http://adresse_ip/

## Télécharger le dernier iso stable de SystemRescueCd
http://www.system-rescue-cd.org/Download

Monter l'image iso dans le système de fichier
sudo mkdir /mnt/iso
sudo mount systemrescuecd-x86-4.8.3.iso /mnt/iso/

## Créer l'arborescence de sysrcd
sudo mkdir /var/lib/tftpboot/sysrcd
sudo mkdir /var/www/sysrcd

y placer les fichiers nécessaires
sudo cp /mnt/iso/isolinux/rescue64 /var/lib/tftpboot/sysrcd/
sudo cp /mnt/iso/isolinux/initram.igz /var/lib/tftpboot/sysrcd/
sudo cp /mnt/iso/sysrcd.dat /var/www/sysrcd/
sudo cp /mnt/iso/sysrcd.md5  /var/www/sysrcd/

## modifier le fichier default de tftpboot

sudo nano /var/lib/tftpboot/pxelinux.cfg/default 

et ajouter un label supplémentaire 

LABEL SRCD
	MENU LABEL SystemRescueCD 4.8.3
	kernel sysrcd/rescue64
	append initrd=sysrcd/initram.igz netboot=http://10.72.9.217/sysrcd/sysrcd.dat setkmap=fr

