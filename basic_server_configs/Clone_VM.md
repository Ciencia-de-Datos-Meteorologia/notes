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
cp /var/lib/libvirt/images/{vm-name}.qcow2 /var/lib/libvirt/images/{clon-vm-name}.qcow2
```

Compress the image
-------------------
gzip /var/lib/libvirt/images/{clon-vm-name}.qcow2

Transfer the disk to the `computer B`
---------------------------------
On the `computer A` run
```
sudo scp /var/lib/libvirt/images/{clon-vm-name}.qcow2.gz user@{computer B's IP}:/var/lib/libvirt/images/
```

Decompress the file
-------------------
On the `computer B` run
```
gunzip {clon-vm-name}.qcow2.gz
```

Create the new VM 
-----------------
Now that we already have the image of the disk on the `computer B`, let's give `libvirt` the access to open the image of the disk
```
sudo chown libvirt-qemu:kvm /var/lib/libvirt/images/{clon-vm-name}.qcow2
sudo chmod 644 /var/lib/libvirt/images/{clon-vm-name}.qcow2
```

Now, finally, we create the clon of the VM with the following command:

```
sudo virt-install \
  --name {VM name} \
  --memory {RAM} \
  --vcpus 2 \
  --disk "path=/var/lib/libvirt/images/{clon-vm-name}.qcow2,format=qcow2,bus=virtio" \
  --os-variant debian11 \
  --import \
  --network bridge=br0,model=virtio \
  --graphics none \
  --console pty
```
