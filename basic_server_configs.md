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

# Configurar pares publico-privados

Sobre la generación de pares de llaves publico-privadas: [Algoritmos y cantidad de bits](https://www.ssh.com/academy/ssh/keygen)

Se deberán generar pares publico-privados utilizando el comando:
```bash
ssh-keygen -t ecdsa -b 521
ssh-copy-id -i ~/.ssh/id_ecdsa user_name@server_ip
```


