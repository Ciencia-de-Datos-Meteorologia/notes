# Editing the `.bashrc` file
There is a file that we can edit if we want to modify the bahavior of our console every time we open a new one. For example, if we want to create functions inside the bash console, this file is the one that we should modify.

To modify the file, we run the command
```
nano ~/.bashrc
```

Once we modified the file, just close it and restart the terminal. You can do it by closing and opening the terminal, or you can execute the following command
```
source ~/.bashrc
```

Here are some usefull functions we could add.

Activate a virtual environment
-----------------------------
```
avenv () {
    # Check if an argument is provided
    if [ -z "$1" ]; then
        deactivate
    else
 source ~/Documents/.python-envs/$1/bin/activate
    fi
}

```
Here, every virtual environment was created on the directory `/home/user/Documents/.python-evns/`.
