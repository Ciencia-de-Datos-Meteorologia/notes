# Install sudo

```
su -
apt-get install sudo
```
To modify the sudoers file, run:

```
visudo
```

Here the user is configured to be able to use `sudo` with some specific privileges. In our case we added the following to the file on the line below the root user permissions:
```
# User privilege specification
root ALL=(ALL:ALL) ALL
data-science ALL=/usr/bin/apt, /usr/bin/apt-get
```
