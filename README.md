### Détection des cartes réseau

```
dmesg |grep eth
eth0: (PCI:33MHz:32-bit) 08:00:27:eb:bb:8b
eth1: (PCI:33MHz:32-bit) 08:00:27:95:12:01
eth0 NIC Link is Up 1000 Mbps Full Duplex, Flow Control: RX
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
    
