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
  - `--location`: Specifies the location of the Ubuntu installation media.
  - `--network`: Connects the virtual machine to the br0 bridge interface.
  - `--graphics none`: Disables the graphical console.
  - `--extra-args`: Passes additional kernel parameters to the installer.


 Access the Virtual machine:
 --------------------------
 
1. If you want to know which virtual machines are created, you can use the following command
   ```
   virsh list
   ```
   
2. When you have chosen which VM you want to access, make sure it is running. If it's not running, start it with:
   ```
   virsh start ubuntu-guest
   ```
   remember to replace `ubunut-guest` with the name of your VM.
   

4. And finally, to access the virtual machine, run the following command:
   ```
   virsh console ubuntu-guest
   ```
   


Possible problems
-----------------
### - Serial console permissions ###

Once the virtual machine is created, it may not be accessible due to serial console permissions. In order to fix this problem you can follow the following steps:

1. Configure the console on the virtual machine:
   - Connect to the VM by another method (if possible) or mount its disk on the host machine to edit the files.
   - Edit the file `/etc/default/grub` inside the VM. Then use the following command:
     
   ```
   sudo nano /etc/default/grub
   ```
   - Find the line that begins with `GRUB_CMDLINE_LINUX_DEFAULT` and add the following options at the end:
   ```
   console=ttyS0 console=tty0
   ```

   It should look like this:
   ```
   GRUB_CMDLINE_LINUX_DEFAULT="quiet splash console=ttyS0 console=tty0"
   ```
   - Now, update grub by running:
   ```
   sudo update-grub
   ```

2. Configure the terminal in systemd:

   Still inside the VM, you must make sure that the serial console service is enabled.
   - Enable the terminal on the serial console (ttyS0):
   ```
   sudo systemctl enable serial-getty@ttyS0.service
   ```
   - Start the service:
   ```
   sudo systemctl start serial-getty@ttyS0.service
   ```

3. Reboot the virtual machine:

   Once the configurations are done, reboot the VM. You can do it by running:
   ```
   virsh reboot ubuntu-guest
   ```

   Note that in this case, `ubuntu-guest` is the name of the virtual machine.

4. Access the console with `virsh`:

   After the VM reboot, you can access the console by running:
   ```
   virsh console ubuntu-guest
   ```
   You should now see console output and be able to interact with the virtual machine from the host terminal.

   
