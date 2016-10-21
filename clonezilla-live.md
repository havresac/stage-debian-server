##Télécharger le dernier iso stable de Clonezilla

http://clonezilla.org/downloads/download.php?branch=stable

Monter l'image iso dans le système de fichier

```
sudo mkdir /mnt/iso
sudo mount clonzilla-live-*.iso /mnt/iso
```

Renommer clonezilla-live-*.iso par le nom de la version que vous venez de télécharger.  

Créer l'arborescence de clonezilla

```
sudo mkdir /var/lib/tftpboot/clonezilla
sudo mkdir /var/lib/tftpboot/clonezilla/live/
```


Placer les fichiers nécessaires au boot de clonezilla depuis le serveur réseau dans le répertoire `/var/lib/tftpboot/`

```
sudo cp /mnt/iso/clonezilla-live-*/live/vmlinuz /var/lib/tftpboot/clonezilla/live/vmlinuz
sudo cp /mnt/iso/clonezilla-live-*/live/initrd.img /var/lib/tftpboot/clonezilla/live/initrd.img
sudo cp /mnt/iso/clonezilla-live-*/filesystem.squashfs /var/lib/tftpboot/clonezilla/live/filesystem.squashfs
```

modifier le fichier default de tftpboot

```
sudo nano /var/lib/tftpboot/pxelinux.cfg/default 
```

et ajouter un label supplémentaire

