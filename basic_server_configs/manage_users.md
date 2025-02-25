If you are managing a server's computer, you might want to know some basic commads. if you want to execute the commands found inside the file, you must enter on `user root`
# Create users
```
useradd -m -s /bin/bash {user's name}
```
where
- `-m`: Create the directory `/home/{user's name}`
- `-s /bin/bash`: Asign `/bin/bash` como su shell predeterminado. 

To asign the new user's password:
```
passwd {user's name}
```

# Modify users
Some usefull options to modify the user's characterictics are:
```
sudo usermod -s /bin/zsh nombre_usuario  # Change the shell tp Zsh
sudo usermod -d /nuevo/home/nombre_usuario nombre_usuario  # Change the home directory
sudo usermod -l nuevo_nombre nombre_usuario  # Change the user's name
sudo usermod -G grupo nombre_usuario  # Add user to a group
```

