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

# Administrar discos duros



# Administrar servidor ssh
