# DNS Server

The purpose of a DNS server is to translate domain names into IP addresses. This is usefull if we are going to access to different computers in the same local network with SSH. In this case we're going to use the service `dnsmasq`.

## Install the server

```
sudo apt update
sudo apt install dnsmasq
```

## Configure the dnsmasq
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

Finally, close and save the file and restart `dnsmasq` to apply the configuration
```
sudo systemctl restart dnsmasq
```

## Configure the clients to use the DNS
If you want that other machines uses the DNS service that you just created, the other computers should edit the `/etc/resolv.conf` file. Here we define what DNS services we want to use, so adding the next line to the file should be enough:
```
nameserver 172.20.3.60
```
Here, `172.20.30.60` is the IP of the machine where we created the DNS service.

