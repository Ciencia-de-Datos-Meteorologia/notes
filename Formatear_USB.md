# Reset a USB on Linux
Locate the USB
------------------
On the bash terminal use the command to know the name of the USB
```
lsblk
```
Its name should be something like `sdX`. where `X` is a letter like `a`, `b`, `c`. 

Once you have located the USB, use the command 
```
sudo umount /dev/sdb
```

Then run the following 
```
sudo mkfs.vfat -F 32 /dev/sdX
```
