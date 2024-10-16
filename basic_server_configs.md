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

# Administrar carpetas de grupos:
Se crearán carpetas de grupos en el directorio `/secs/`, el dueño de estas carpetas será `root` y el grupo dueño de cada una será el grupo correspondiente. Además, para heredar el grupo a cualquier archivo creado dentro de ellas sin importar el usuario que lo cree (podría ser un usuario externo al grupo) se deberá configurar el `setgid` a la carpeta, además de quitar todos los permisos para usuarios externos al grupo, esto se realiza:

```bash
mkdir /secs/sec_name/
chmod 2770 /secs/sec_name/
```

Donde el primer bit representa la configuración de `setgid` y los otros son los usuales permisos para el dueño, grupo y otros.

# Administrar `umask`:
Se configurará `umask 002` como máscara de permisos por defecto (resulta en permisos `775`) para todos los usuarios, para esto se debe agregar `umask 002` al archivo `vi /etc/profile.d/set-umask-for-all-users.sh` (crearo en caso de no existir).

-------
# Llave público-privada

Sobre la generación de pares de llaves publico-privadas: [Algoritmos y cantidad de bits](https://www.ssh.com/academy/ssh/keygen)

Se deberán generar pares publico-privados utilizando el comando:
```bash
ssh-keygen -t ecdsa -b 521
ssh-copy-id -i ~/.ssh/id_ecdsa user_name@server_ip
```


