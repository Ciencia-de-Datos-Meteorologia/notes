# Creating a SSH Dinamic Tunel guide

This guide give you all the necesary steps to configure a dinamic tunel using SSH. This method allows you to access all available IP addresses on the local network of a remote computer.

## Step 1: Creating the Dinamic Tunel
Open a terminal on the local machine and execute the following comand
```
ssh -D 1080 user@remote_server
```
where
  - -D 1080: COnfigure a SOCKS proxy on the 1080 port of the local machine.
  - user: It's the name of the user on the remote machine.
  - remote_server: It's the IP address or domain name of the remote machine.

-Note : Do NOT close the terminal to keep the address active.
