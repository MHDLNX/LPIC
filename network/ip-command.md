The `ip` command in Linux is a powerful tool used for network management. It is part of the iproute2 package and replaces older networking tools like `ifconfig`, `route`, and `netstat`. The `ip` command can be used to configure network interfaces, manage routing tables, and display network information.

### Common Subcommands of `ip`

1. **ip link**: Manage network interfaces.
2. **ip addr**: Manage IP addresses.
3. **ip route**: Manage routing tables.
4. **ip neigh**: Manage ARP (Address Resolution Protocol) entries.
5. **ip rule**: Manage policy routing rules.

### Examples

#### 1. Displaying Network Interfaces

**Example**: Display all network interfaces and their statuses.

```bash
ip link show
```

Output might look like:

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP mode DEFAULT group default qlen 1000
    link/ether 00:1a:2b:3c:4d:5e brd ff:ff:ff:ff:ff:ff
```

#### 2. Bringing an Interface Up or Down

**Example**: Bring the `eth0` interface down.

```bash
ip link set eth0 down
```

**Example**: Bring the `eth0` interface up.

```bash
ip link set eth0 up
```

#### 3. Displaying IP Addresses

**Example**: Show all IP addresses assigned to all interfaces.

```bash
ip addr show
```

Output might look like:

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:1a:2b:3c:4d:5e brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.100/24 brd 192.168.1.255 scope global dynamic eth0
       valid_lft 86391sec preferred_lft 86391sec
    inet6 fe80::21a:2bff:fe3c:4d5e/64 scope link 
       valid_lft forever preferred_lft forever
```

#### 4. Adding and Deleting IP Addresses

**Example**: Add an IP address to the `eth0` interface.

```bash
ip addr add 192.168.1.101/24 dev eth0
```

**Example**: Delete an IP address from the `eth0` interface.

```bash
ip addr del 192.168.1.101/24 dev eth0
```

#### 5. Displaying and Configuring Routes

**Example**: Display the routing table.

```bash
ip route show
```

Output might look like:

```
default via 192.168.1.1 dev eth0 proto dhcp metric 100 
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.100 metric 100
```

**Example**: Add a default route via a specific gateway.

```bash
ip route add default via 192.168.1.1
```

**Example**: Delete a specific route.

```bash
ip route del 192.168.1.0/24 dev eth0
```

#### 6. Managing ARP Entries

**Example**: Display the ARP table.

```bash
ip neigh show
```

Output might look like:

```
192.168.1.1 dev eth0 lladdr 00:1a:2b:3c:4d:5e REACHABLE
```

**Example**: Add a static ARP entry.

```bash
ip neigh add 192.168.1.2 lladdr 00:1b:2c:3d:4e:5f dev eth0
```

**Example**: Delete an ARP entry.

```bash
ip neigh del 192.168.1.2 dev eth0
```

### Summary

The `ip` command is a versatile and powerful tool for network management in Linux. Its various subcommands allow you to manage interfaces, IP addresses, routes, and ARP tables comprehensively. These examples should help you understand how to use the `ip` command in different scenarios.
