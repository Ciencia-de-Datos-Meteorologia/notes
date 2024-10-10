Estas instrucciones están pensadas desde un usuario, en el caso de ser root se puede omitir las líneas `su -` y los comandos que utilicen `sudo`.

# Instalar sudo

```bash
su -
apt-get install sudo

visudo
```

Acá se configura al usuario para poder utilizar `sudo` con algunos privilegios específicos. En nuestro caso agregamos al archivo lo siguiente en la línea debajo de los permisos del usuario root:

```bash
# User privilege specification
root ALL=(ALL:ALL) ALL
data-science ALL=/usr/bin/apt, /usr/bin/apt-get
```

# Instalar sugerencias de paquetería

```bash
sudo apt install command-not-found
apt-file update
update-command-not-found
```

# Modificar configuración de red
Se debe editar el archivo `/etc/network/interfaces` como super usuario. La estructura del archivo es la siguiente:

```bash
sudo nano /etc/network/interfaces
```

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

# Create a public-provite key paor for SSH to use with GitHub

## 1. Check if you already have SSH keys set up:
   ```
   ls -al ~/.ssh
   ```
   If you see files like `id_rsa.pub` or `id_ed25510.pub`, you might already have an SSH key. If not, you can create one.

## 2. Generate a new SSH key
   You can generate a new SSH key using the `ssh-keygen` command:
   ```
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
- `-t ed25519` especifies the type of key.
- `-C your_email@example.com` adds a comment, wich is typically your email.

  If your system doesn't support `ed25519`, use
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
ssh-add ~/.ssh/id_ed25519
```
(Replace `id_ed25519` with the name of your key file if different.)

## 4. Add the SSH key to your GitHub account

You need to add your public key (not the private key) to GitHub.

- Copy the public key to your clipboard:
  ```
  cat ~/.ssh/id_ed25519.pub
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


