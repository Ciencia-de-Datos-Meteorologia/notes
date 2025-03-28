# Procesos en segundo plano
En algunos casos específicos será necesario que un proceso se ejecute de manera permanente, pero si se ejecuta de manera normal, cada vez que se cierre la terminal desde la que se ejecuta, el proceso se cancelará. Por esto es recomendable que el proceso se ejecute en segundo plano. Para hacerlo basta con utilizar el comando 

```
nohup python3 tu_script.py > output.log 2>&1 &
```
donde 
- `nohup` evita que el proceso se detenga si se cierra la terminal.
- `> output.log 2>&1` redirige la salida del script a un archivo (`output.log`).
- `&` lo ejecuta en segundo plano.


Visualizar procesos 
-----------------

Para ver el proceso en ejecución utiliza el comando:
```
ps aux | grep tu_script.py
```

Si necesistas detener el proceso, utiliza
```
kill <PID>
```
donde `<PID>` es el ID del proceso que puedes encontrar con el comando anterior.

Servicios permanentes
---------------------

En caso de que el proceso utilice Flask, se puede hacer que el proceso inicie automaticamente cada vez que se enciende la computadora. Para esto crea un archivo en `/etc/systemd/system/flask_app.service` con
```
[Unit]
Description=Mi aplicación Flask
After=network.target

[Service]
User=tu_usuario
WorkingDirectory=/ruta/del/script
ExecStart=/usr/bin/python3 tu_script.py
Restart=always

[Install]
WantedBy=multi-user.target
```

Luego, ejecuta 
```
sudo systemctl daemon-reload
sudo systemctl enable flask_app
sudo systemctl start flask_app
```

Para ver el estado del servicio 
```
sudo systemctl status flask_app
```

Y para detenerlos
```
sudo systemctl stop flask_app
```
