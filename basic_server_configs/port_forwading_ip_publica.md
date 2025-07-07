# Túnel SSH Persistente con autossh y systemd

Este repositorio contiene instrucciones y archivos para crear un túnel SSH remoto persistente usando `autossh` como servicio `systemd`. Así garantizamos que la conexión se mantenga activa y se reconecte automáticamente si se cae o si la máquina se reinicia.

---

## ¿Para qué sirve?

- Permite exponer un puerto local (ejemplo: Grafana corriendo en `localhost:5000`) en un servidor remoto.
- Mantiene la conexión abierta y se reconecta automáticamente.
- El túnel se inicia automáticamente con el sistema y se reinicia si falla.

---

## Requisitos

- Máquina cliente (donde corre el servicio que quieres exponer en el túnel).
- Servidor remoto con acceso SSH.
- `autossh` instalado en la máquina cliente.
- Permisos para editar y recargar servicios `systemd` en la máquina cliente.
- Configuración del servidor SSH remoto que permita `AllowTcpForwarding`.
- Colocar llave ssh de la computadora local en la computadora con ip publica
---

## Pasos para configurar el túnel persistente

### 1. Instalar `autossh`

En la máquina cliente (ejemplo Debian/Ubuntu):

```bash
sudo apt update
sudo apt install autossh
```
2. Crear el archivo del servicio systemd

Crea un archivo llamado autossh-tunnel.service en /etc/systemd/system/:

Pega el siguiente contenido, ajustando las variables REMOTE_USER, REMOTE_HOST, REMOTE_PORT y LOCAL_PORT según tu caso:

[Unit]
Description=AutoSSH túnel SSH persistente
After=network.target

[Service]
User=tu_usuario_local
Environment="AUTOSSH_GATETIME=0"
Environment="AUTOSSH_POLL=60"
Environment="AUTOSSH_LOGFILE=/home/tu_usuario_local/autossh.log"
ExecStart=/usr/bin/autossh -M 0 \
    -o ServerAliveInterval=60 \
    -o ServerAliveCountMax=3 \
    -o StrictHostKeyChecking=no \
    -o ExitOnForwardFailure=yes \
    -N -R REMOTE_PORT:localhost:LOCAL_PORT REMOTE_USER@REMOTE_HOST
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target

Si quieres exponer localmente localhost:5000 en el servidor remoto 138.118.104.87 en el puerto 5000, y tu usuario local es data-base, el ExecStart sería:
```
ExecStart=/usr/bin/autossh -M 0 \
    -o ServerAliveInterval=60 \
    -o ServerAliveCountMax=3 \
    -o StrictHostKeyChecking=no \
    -o ExitOnForwardFailure=yes \
    -N -R 5000:localhost:5000 sensores@138.118.104.87
```
3. Recargar systemd y habilitar el servicio

```
sudo systemctl daemon-reload
sudo systemctl enable autossh-tunnel.service
sudo systemctl start autossh-tunnel.service
```
4. Verificar que el servicio está activo y funcionando
```
sudo systemctl status autossh-tunnel.service
tail -f /home/tu_usuario_local/autossh.log
```
5. Comprobar en el servidor remoto

En el servidor remoto, verifica que el puerto remoto está escuchando:
```
sudo netstat -tulnp | grep REMOTE_PORT
```
Notas importantes

El servidor SSH remoto debe permitir el reenvío de puertos. Para eso, en /etc/ssh/sshd_config en el servidor remoto, asegúrate que estén configuradas estas líneas:
```
AllowTcpForwarding yes
GatewayPorts yes
PermitOpen any
```
Y reinicia el SSH:
```
sudo systemctl restart ssh
```
