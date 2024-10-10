Creating the Virtual machine
----------------------------

1. Install the necessary packages:
   ```
   sudo apt-get update
   sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils
   ```
2. Create a new virtual machine:
   ```
   sudo virt-install \
   --name ubuntu-guest \
   --os-variant ubuntu20.04 \
   --vcpus 2 \
   --ram 4096 \
   --location http://ftp.ubuntu.com/ubuntu/dists/focal/main/installer-amd64/ \
   --network bridge=br0,model=virtio \
   --graphics none \
   --extra-args='console=ttyS0,115200n8 serial'
   ```
  Explanation of the options:
  - `--name`: Specifies the name of the virtual machine.
  - `--os-variant`: Specifies the operating system type and variant (Ubuntu 20.04 in this case).
  - `--vcpus`: Allocates 2 virtual CPUs to the virtual machine.
  - `--ram`: Allocates 4GB of RAM to the virtual machine.
  - `--location`: Specifies the location of the Ubuntu Server installation media.
  - `--network`: Connects the virtual machine to the br0 bridge interface.
  - `--graphics none`: Disables the graphical console.
  - `--extra-args`: Passes additional kernel parameters to the installer.
   
