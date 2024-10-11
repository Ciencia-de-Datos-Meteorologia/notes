# Modify network settings 
If you want to modify the IP, netmask, gateway or network port, you must edit the `/etc/network/interfaces` file as sudo. 

To edit the file,

```bash
sudo nano /etc/network/interfaces
```

The file must seem like this:
```bash
# interfaces(5) file used by ifup(8) and ifdown(8)
# Include files from /etc/network/interfaces.d:
source /etc/network/interfaces.d/*

iface eno1 inet manual

auto brlan
iface brlan inet static
      address 172.20.3.55
      netmask 255.255.255.192
      gateway 172.20.3.1
      dns-nameserver 172.20.1.66
      dns-nameserver 8.8.8.8
```
Then, to aply the changes, run the next command
```bash
sudo systemctl restart networking
```
