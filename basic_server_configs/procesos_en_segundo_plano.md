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
