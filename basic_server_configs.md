These instructions are intended for a user, if you are root you can omit the `su -` lines and the commands that use `sudo`.

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


-------
# Llave público-privada

Sobre la generación de pares de llaves publico-privadas: [Algoritmos y cantidad de bits](https://www.ssh.com/academy/ssh/keygen)

Se deberán generar pares publico-privados utilizando el comando:
```bash
ssh-keygen -t ecdsa -b 521
ssh-copy-id -i ~/.ssh/id_ecdsa user_name@server_ip
```


