El comando para clonar el disco `sda` de una computadora hacia el disco `sdb` de otra computadora es:
```
sudo dd if=/dev/sda bs=4M | ssh usuario@IP_destino "sudo dd of=/dev/sdb bs=4M status=progress"
```

Zuko
-----
En el caso específico de Zuko, los archivos que modifiqué fueron
- visudo
- chmod /dev/sda 660
- /etc/ssh/sshd_config
- /etc/network/interfaces
  Normalmente se ve así
```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

auto eno1
iface eno1 inet manual

# Bridge interface
auto br0
iface br0 inet static
#allow-hotplug eno1 
#iface eno1 inet static
        address 172.20.3.60
        netmask 255.255.255.0
        gateway 172.20.3.1
        dns-nameservers 172.20.1.66 8.8.8.8
        bridge_ports eno1
        bridge_stp off
        bridge_fd 0
        bridge_maxwait 0

```
  Pero para clonar lo modifiqué así
```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

#auto eno1
#iface eno1 inet manual

# Bridge interface
#auto br0
#iface br0 inet static
allow-hotplug eno1 
iface eno1 inet static
        address 172.20.3.60
        netmask 255.255.255.0
        gateway 172.20.3.1
        dns-nameservers 172.20.1.66 8.8.8.8
        bridge_ports eno1
        bridge_stp off
        bridge_fd 0
        bridge_maxwait 0
```

  

