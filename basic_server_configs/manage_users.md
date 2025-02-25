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
