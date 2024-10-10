These instructions are intended for a user, if you are root you can omit the `su -` lines and the commands that use `sudo`.

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

# Install package suggestions
This package helps when you have an idea of the command but you don't know it, so it suggests similar commands.

```bash
sudo apt install command-not-found
apt-file update
update-command-not-found
```

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

Después ejectuar:
```bash
sudo systemctl restart networking
```

# Administrar discos duros



# Administrar servidor ssh

# Administrar usuarios:
Para crear un usuario nuevo se debe ejecutar como administrador:
```bash
useradd -m -g aplicaciones_climaticas -s /bin/bash {new_user_name}
passwd {new_user_name}
```

Los usuarios podrán cambiar su contraseña usando `passwd {user_name}` y su shell usando `chsh`.

Para crear un grupo se usa `groupadd`.

# Create a public-private key pair for SSH to use with GitHub

## 1. Check if you already have SSH keys set up:
   ```
   ls -al ~/.ssh
   ```
   If you see files like `id_rsa.pub` or `id_ed25510.pub`, you might already have an SSH key. If not, you can create one.

## 2. Generate a new SSH key
   You can generate a new SSH key using the `ssh-keygen` command:
   ```
   ssh-keygen -t ecdsa -b 521
   ```
- `-t ecdsa` especifies the type of key.
- `-b 521` is the size of the key.

  If your system doesn't support `ecdsa`, use
  ```
  ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
  ```

  After running the command:

- When prompted to "Enter a file in which to save the key," you can press Enter to use the default location (`~/.ssh/id_ed25519` or `~/.ssh/id_rsa`).
- Optionally, add a passphrase for extra security, or just press Enter for no passphrase.


## 3. Add your SSH key to the SSH agent

Start SSH agent
```
eval "$(ssh-agent -s)"
```

Then add your SSH private key to the SSH agent
```
ssh-add ~/.ssh/id_ecdsa
```
(Replace `id_ecdsa` with the name of your key file if different.)

## 4. Add the SSH key to your GitHub account

You need to add your public key (not the private key) to GitHub.

- Copy the public key to your clipboard:
  ```
  cat ~/.ssh/id_ecdsa.pub
  ```
  Copy the entire output.
- Go to your [GitHub SSH settings](https://github.com/settings/keys) and click "New SSH key".
- Paste the key into the "Key" field, and give it a title.
- Click "Add SSH key".


## 5. Test your SSH connection
Finally, test your SSH connection to GitHub:
```
ssh -T git@github.com
```

If everything is set up correctly, you will see a success message similar to:
```
Hi username! You've successfully authenticated, but Github does not provide shell access.
```

-------

Sobre la generación de pares de llaves publico-privadas: [Algoritmos y cantidad de bits](https://www.ssh.com/academy/ssh/keygen)

Se deberán generar pares publico-privados utilizando el comando:
```bash
ssh-keygen -t ecdsa -b 521
ssh-copy-id -i ~/.ssh/id_ecdsa user_name@server_ip
```


