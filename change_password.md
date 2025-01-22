# Change the user's password on Debian
In some cases, you must want to replace the old password with a new one. It doesn't matter what type of user you are (user or root), the process to update the password is very simple. 
First of all, you must be on a terminal with the `user` session on. If you are on a user session and you wish to switch to the root user, just use the Switch User command:
```
su -
```

Then all you have to do is run the command
```
passwd
```
After this, the terminal will ask you to type the new password. When the message `passswd: password updated successfully` is out, the process is done.

# Change the computer's name
If your computer has some default name like `debian` or simply you just don't like the name, you can update the computer's name. This is done by modifying 2 files, `/etc/hostname` and `/etc/hosts`. 

To access a file, use the command `nano`, for example
```
sudo nano /etc/hostname
```
In this file you'll only find the computer's name, so erase it and add the one you like. Then press `Ctrl+O` and `Ctrl+X` to save and exit.  

After this, open the next file
```
sudo nano /etc/hosts
```
You'll see the computer's name to the right of the IP `127.0.1.1`. Erase this name and add the one you have chosen before. And that's it, your computer now has a different name.
