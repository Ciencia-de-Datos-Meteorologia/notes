#DNS Server#

The purpose of a DNS server is to translate domain names into IP addresses. This is usefull if we are going to access to different computers in the same local network with SSH. In this case we're going to use the service `dnsmasq`.

##Install the server##

```
sudo apt update
sudo apt install dnsmasq
```

##Configure the dnsmasq
Open the file `/etc/dnsmasq.conf`
```
sudo nano /etc/dnsmasq.conf
```
Then add the IPs and the alias you want to asign to each one. It should look like this:
```
address=/Computer1/172.20.3.61
address=/Computer2/172.20.3.62
address=/Computer3/172.20.3.63
```
Where `Computer1` is the alias you want to asign to the IP 172.20.3.61
