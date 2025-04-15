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
