There is a file that we can edit if we want to modify the bahavior of our console every time we open a new one. For example, if we want to create functions inside the bash console, this file is the one that we should modify.

To modify the file, we run the command
```
nano ~/.bashrc
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
 source ~/Documents/.python-envs/$1/bin/activate  # commented out by conda initialize
    fi
}

```
