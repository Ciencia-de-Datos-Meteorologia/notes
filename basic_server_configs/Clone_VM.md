# Clone a Virtual Machine
If some day you wake up and feel a wish to clone a virtual machine and place it into other physical computer, this is a list of steps you must follow.

First, let's assume the `computer A` is the computer where the virtual machine is located, and `computer B` is the computer where we want to install the VM. 

Find the VM's disk
------------------------
```
sudo virsh domblklist {vm-name}
```
you'll see something like 

```
Target     Source
------------------------------------------------
vda        /var/lib/libvirt/images/{vm-name}.qcow2
```


Clone the disk
--------------
First, shut down the VM
```
virsh shutdown {vm-name}
```
once it's down, clone the disk
```
cp /var/lib/libvirt/images/{vm-name}.qcow2 /var/lib/libvirt/images/{clone-vm-name}.qcow2
```
