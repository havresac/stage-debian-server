## But
Créer un serveur PXE permettant la mise à dispositions d'outils sans supports (![schema global](https://github.com/havresac/stage-debian-server/blob/master/img/schema.svg))

> __Notions préliminaires :__

> Le serveur PXE (Preboot eXecution Environment, environnement de démarrage d'ordinateurs en réseau) aura ici pour but de fournir aux postes clients connectés en réseau local une image ISO bootable en vue du déploiement d'images disque. 

Le serveur PXE utilise Debian GNU/Linux en tant que système d'exploitation.


### Détection des cartes réseau

```
dmesg |grep eth
eth0: (PCI:33MHz:32-bit) 08:00:27:eb:bb:8b
eth1: (PCI:33MHz:32-bit) 08:00:27:95:12:01
eth0 NIC Link is Up 1000 Mbps Full Duplex, Flow Control: RX
```
### Configuration de eth1
```
sudo nano /etc/network/interfaces
# The primary network interface
auto eth0
iface eth0 inet dhcp

iface eth1 inet static
        address 192.168.42.1
        netmask 255.255.255.0
```

### Installation du service isc-dhcp-server
```
sudo apt-get install isc-dhcp-server

sudo nano /etc/dhcp/dhcpd.conf

    #option domain-name "example.org";
    #option domain-name-servers ns1.example.org, ns2.example.org;

    authoritative;

    subnet 192.168.42.0 netmask 255.255.255.0 {
    	range 192.168.42.10 192.168.42.50;
    	option broadcast-address 192.168.42.255;
    	option routers 192.168.42.1;
    	default-lease-time 600;
    	max-lease-time 7200;
    	option domain-name "local";
    	option domain-name-servers 8.8.8.8, 8.8.4.4;
    }
```

### Configuration du port réseau utilisé
```
sudo nano /etc/default/isc-dhcp-server

INTERFACES="eth1"
```
### Démarrage du service
```
sudo service isc-dhcp-server start
```

### Démarrage du client
```
Oct 17 10:51:24 sidsic-stage1 dhcpd: Wrote 0 leases to leases file.
Oct 17 10:51:52 sidsic-stage1 dhcpd: DHCPDISCOVER from 08:00:27:3c:2e:7d via eth1
```

## Serveur PXE & Service TFTP

Installation et Configuration du [serveur PXE et du service TFTP] (https://github.com/havresac/stage-debian-server/blob/master/pxe-tftp.md)

## Lighttpd & SystemRescueCd

Installation d'un [serveur web léger] (https://github.com/havresac/stage-debian-server/blob/master/SystemRescueCd.md) et préparation et mise en place d'une image [SystemRescueCd](https://github.com/havresac/stage-debian-server/blob/master/SystemRescueCd.md#t%C3%A9l%C3%A9charger-le-dernier-iso-stable-de-systemrescuecd)

## Clonezilla

Préparation et mise en place d'une image [Clonezilla] (https://github.com/havresac/stage-debian-server/blob/master/clonezilla-live.md)

