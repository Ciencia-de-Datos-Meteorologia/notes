# Make a backup properly 
First you must mount the disk where you are going to save the backup. To know the name of the disk use the command
```
lsblk
```

and you'll find a list of all disks connected. Let's asume the disk's name is `sdX2`. Then, create a mount point 
```
cd
mkdir -p /mnt/backup
```
and mount the partition 
```
mount /dev/sdX2 /mnt/backup
```

Option 1
--------

One option to create a backup on a external disk is using the `rsync` command. 
```
sudo rsync -aAXv / --exclude={"/proc","/sys","/dev","/run","/tmp","/mnt","/media","/lost+found"} /mnt/backup
```

Option 2
--------

Use the same command but only specify which directories you want
```
sudo rsync -aAXv /var /etc /home/data-science/automatizacion_bash/ /home/data-science/.config/ /home/data-science/.gitconfig/ /home/data-science/interfaz_database/ /home/data-science/mapaClima/ /mnt/backup/ZUKO
```
where the last path is where the backup will be saved.

### Note
For some reason, the images of the virtual machines are not copying right, so I convine the 2 options like this 
```
sudo rsync -av --exclude=var/lib/libvirt/images/ /var /etc /home/data-science/automatizacion_bash/ /home/data-science/.config/ /home/data-science/.gitconfig/ /home/data-science/interfaz_database/ /home/data-science/mapaClima/ /mnt/backup/ZUKO
```

And then copy the VM manually with
```
sudo cp /var/lib/libvirt/images/{vm-name} /mnt/backup/ZUKO/var/lib/libvirt/images/
```
