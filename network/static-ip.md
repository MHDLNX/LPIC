To change a network interface from using DHCP to a static IP address, you will need to edit the network configuration files on your system. The steps vary slightly depending on the operating system you are using. Here are the instructions for both Linux and Windows:

### On Linux (e.g., Ubuntu/Debian)

1. **Identify the Network Interface**: Use the command `ip a` or `ifconfig` to list the network interfaces and identify the one you want to configure.

2. **Edit the Network Configuration File**: The location of this file depends on the distribution and version. For recent versions of Ubuntu (using `netplan`), you would edit a `.yaml` file in `/etc/netplan/`.

   - Open the terminal.
   - Edit the network configuration file using a text editor. For example, `sudo nano /etc/netplan/01-netcfg.yaml` (the exact file name may vary).

3. **Configure Static IP**: Modify the file to configure the interface with a static IP address. For example:

   ```yaml
   network:
     version: 2
     ethernets:
       eth0:
         dhcp4: no
         addresses: [192.168.1.100/24]
         gateway4: 192.168.1.1
         nameservers:
           addresses: [8.8.8.8, 8.8.4.4]
   ```

4. **Apply the Configuration**: Save the file and apply the changes with the command `sudo netplan apply`.
