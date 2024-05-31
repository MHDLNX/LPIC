The `ip` command is a powerful utility for network configuration and management in Linux. It is part of the `iproute2` package and can be used to manage network interfaces, routing tables, and more. Here are some common uses of the `ip` command with examples:

### Viewing Network Interfaces

1. **List all network interfaces:**
   ```bash
   ip link show
   ```
   This command displays detailed information about all network interfaces.

2. **Show detailed information for a specific interface:**
   ```bash
   ip link show dev eth0
   ```
   Replace `eth0` with the name of your network interface.

### Managing Network Interfaces

3. **Bring an interface up:**
   ```bash
   sudo ip link set dev eth0 up
   ```
   This command activates the network interface.

4. **Bring an interface down:**
   ```bash
   sudo ip link set dev eth0 down
   ```
   This command deactivates the network interface.

### IP Addresses

5. **Show IP addresses assigned to all interfaces:**
   ```bash
   ip addr show
   ```

6. **Show IP addresses for a specific interface:**
   ```bash
   ip addr show dev eth0
   ```

7. **Assign an IP address to an interface:**
   ```bash
   sudo ip addr add 192.168.1.100/24 dev eth0
   ```
   This command assigns the IP address `192.168.1.100` with a subnet mask of `255.255.255.0` to the interface `eth0`.

8. **Remove an IP address from an interface:**
   ```bash
   sudo ip addr del 192.168.1.100/24 dev eth0
   ```

### Routes

9. **Show the routing table:**
   ```bash
   ip route show
   ```

10. **Add a route:**
    ```bash
    sudo ip route add 192.168.2.0/24 via 192.168.1.1 dev eth0
    ```
    This command adds a route to the `192.168.2.0/24` network via the gateway `192.168.1.1` on the interface `eth0`.

11. **Delete a route:**
    ```bash
    sudo ip route del 192.168.2.0/24
    ```

### Neighbors (ARP)

12. **Show neighbor/ARP table:**
    ```bash
    ip neigh show
    ```

13. **Add an ARP entry:**
    ```bash
    sudo ip neigh add 192.168.1.10 lladdr 00:11:22:33:44:55 dev eth0
    ```

14. **Delete an ARP entry:**
    ```bash
    sudo ip neigh del 192.168.1.10 dev eth0
    ```

### Examples for Specific Use Cases

#### Configuring a Static IP Address

1. **Bring the interface down:**
   ```bash
   sudo ip link set dev eth0 down
   ```

2. **Assign a new IP address:**
   ```bash
   sudo ip addr add 192.168.1.100/24 dev eth0
   ```

3. **Bring the interface up:**
   ```bash
   sudo ip link set dev eth0 up
   ```

4. **Add a default gateway:**
   ```bash
   sudo ip route add default via 192.168.1.1
   ```

#### Viewing and Flushing IP Addresses

1. **View all IP addresses on all interfaces:**
   ```bash
   ip addr
   ```

2. **Flush all IP addresses on a specific interface:**
   ```bash
   sudo ip addr flush dev eth0
   ```

### Summary

The `ip` command is a versatile tool for network management on Linux systems, providing comprehensive control over interfaces, IP addresses, routes, and more. Here are the key commands to remember:

- **List interfaces**: `ip link show`
- **Assign IP address**: `sudo ip addr add 192.168.1.100/24 dev eth0`
- **Show IP addresses**: `ip addr show`
- **Manage routes**: `ip route show`, `sudo ip route add`, `sudo ip route del`
- **Manage ARP**: `ip neigh show`, `sudo ip neigh add`, `sudo ip neigh del`

These examples cover the most common tasks, making `ip` an essential command for network administration in Linux.
