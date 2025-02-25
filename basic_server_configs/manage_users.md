If you are managing a server's computer, you might want to know some basic commads. if you want to execute the commands found inside the file, you must enter on `user root`

Users
-------

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
# Delete users
```
userdel -r {user's name}
```
- `-r`: Delete the user and his directory `/home/{user's name}`

Groups 
-------
A group is a collection of user accounts that share certain permissions and privileges over some files, directories and resorces of the system.

# Examples 

Let's assume many users need access to  '/opt/meteorologia'. Insted of assingning permissions to each user, you can create a group:
```
sudo groupadd meteorologos
sudo chown :meteorologos /opt/meteorologia
sudo chmod 770 /opt/meteorologia
sudo usermod -aG meteorologos usuario1
```


# Create groups
```
group add {group's name}
```

# Add user to a group 
```
usermod -aG {group's name} {user's name}
```
where
-  `-aG`: Append the user without removiming it from other groups.

# Delete user from group

```
gpasswd -d {user's name} {group's name}
```

# Delete group
```
groupdel {group's name}
```

