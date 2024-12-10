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

Note : Do NOT close the terminal to keep the address active.

## Step 2: Configure the navegator to use the SOCKS proxy 
Configure the browser to redirect traffic through the SOCKS proxy.

Firefox
-------
1. Settings -> General -> Network configuration
2. Select 'Manual proxy configuration'
3. Change the following items
  - **Host SOCKS**: localhost
  - **Port**: 1080
4. Check the SOCKS v5 Proxy option
5. Save the changes

Google Chrome or Chromium
------------------
Open Chrome from the terminal:
```
google-chrome --proxy-server="socks5://localhost:1080"
```

## Step 3: Access the local IP addresses
Once the proxy is configured, any request made from the browser will go through the SSH tunnel and local IP addresses will be visible.
