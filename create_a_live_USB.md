# Create a bootable USB

Debian 12
--------
Download the ISO image of the installer. You can find it on [Debian's website](https://www.debian.org/download) or directly on this [link](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-12.8.0-amd64-netinst.iso).

Locate the USB you are going to use
```
lsblsk
```
For the example above, let's assume the USB's name is `sdc`.

Move to the `Downloads` directory
```
cd ~/Downloads
ls -lh
```

To write the ISO image of Debian on the USB, run the following command
```
sudo dd if=debian-12.0.0-amd64-netinst.iso of=/dev/sdb bs=1M status=progress conv=noerror,sync
```
where `debian-12.0.0-amd64-netinst.iso` is the name of the ISO.
