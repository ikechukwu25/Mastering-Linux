# NETWORKING IN LINUX

Networking in Linux encompasses a wide array of activities, ranging from configuring basic network settings to managing network interfaces. It also involves establishing connections, and troubleshooting network issues. 

### NETWORK INTERFACES 

Understanding and managing network interfaces is essential for configuring and troubleshooting network connections in Linux systems. 
To gather information about network interfaces in Linux, two commonly used commands are `ifconfig` and `ip`.

`ifconfig` 

`ifconfig -a` = Displays information about all network interfaces, including both enabled and disabled ones.
Note: `ifconfig` is part of the net-tools package, which may need to be installed separately (`sudo apt install net-tools` on Debian-based systems).

`ip`

`ip address show` = Displays detailed information about network interfaces.

Both `ifconfig` and `ip address show` provide similar output, typically listing interfaces such as enp0s3 (Ethernet interface) and lo (Loopback interface).

To obtain specific information about a particular interface, you can use commands like ifconfig <interface-name> or ip address show dev <interface-name>.
For example, `ifconfig enp0s3` or `ip address show dev enp0s3`

`route`

The route command is primarily used to display and manipulate the IP routing table on Linux systems, which includes information about network routes and gateways. It provides details about how network packets should be forwarded to their destinations.

To ensure proper communication on the internet, a system requires a default gateway, which serves as the exit point for traffic leaving the local network. The default gateway is typically configured as part of the network settings and is crucial for routing packets to destinations outside the local subnet.

The `route` command, available in the net-tools package, is commonly used to display and manipulate the IP routing table on Linux systems. When used without options, the `route` command provides a human-readable output showing the routing table, including the default gateway.

Here's an example of the output from the route command:

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use | Iface |
|--------|--------|--------|--------|--------|--------|--------|--------|
| 0.0.0.0 | 192.168.64.1 | 0.0.0.0 | UG | 100 | 0 | 0 | enp0s1 |

In this output:

Destination: The destination network or address. For the default gateway, it's represented as 0.0.0.0, indicating all destinations not explicitly defined in the routing table.
Gateway: The IP address of the default gateway.
Genmask: The netmask associated with the destination network.
Flags: The routing flags, where UG indicates that the route is a gateway route (default gateway).
Metric: The metric or cost associated with the route.
Ref: Reference count for the route.
Use: Number of times the route has been used.
Iface: The network interface associated with the route.


### NETWORK CONFIGURATION

Network configuration in Linux involves setting up and managing network interfaces, establishing connections, and configuring network-related parameters such as IP addresses, routes, DNS servers, and more. This is essential for enabling communication between devices on a network and accessing the internet. Tools like `ifconfig`, `ip`, `route`, `systemd-networkd`, `NetworkManager`, and configuration files such as /etc/network/interfaces or /etc/sysconfig/network-scripts/ifcfg-* are commonly used to manage network settings in Linux systems. Proper network configuration ensures reliable connectivity and efficient data transmission across networks.

| Term | Definition |
|----------|----------|
| Router |	Also called a gateway, a router is a machine that connects hosts from one network to another network. For example, if you work in an office environment, the computers within the company can all communicate via the local network created by the administrators. To access the Internet, the computers would have to communicate with a router that would be used to forward network communications to the Internet. Typically when you communicate on a large network (like the Internet), several routers are used before your communication reaches its final destination. |
| Mask |	Also called a netmask, subnet mask, or mask, a network mask is a number system that can be used to define which IP addresses are considered to be within a single network. Because of how routers perform their functions, networks have to be clearly defined. </br> Let's say you want to group houses together based on their location. You might use something like a street or neighborhood name to group them. In computer networks, we use something called a netmask to group IP addresses together based on their network. |
| Packet |	A network packet is used to send network communication between hosts. By breaking down communication into smaller chunks (packets), the data delivery method is much more efficient. |
| DHCP |	Hosts can be assigned hostnames, IP addresses, and other network-related information by a DHCP (Dynamic Host Configuration Protocol) server. In the world of computers, a protocol is a well-defined set of rules. DHCP defines how network information is assigned to client hosts, and the DHCP server is the machine that provides this information. |
| DNS	| As mentioned previously, hostnames are translated into IP addresses, prior to the network packet being sent on the network. So your host needs to know the IP address of all of the other hosts with which you are communicating. When working on a large network (like the Internet), this can pose a challenge as there are so many hosts. A Domain Name System (DNS) provides the service of translating domain names into IP addresses. </br> DNS is like a giant phonebook for the internet. It translates human-readable domain names, like "google.com" or "facebook.com," into IP addresses, which are unique numerical addresses that computers use to identify each other on the internet. So, when you type a web address into your browser, your computer uses DNS to look up the corresponding IP address and connect you to the correct website. |
| TCP/IP |	The Transmission Control Protocol/Internet Protocol (TCP/IP) is a fancy name for a collection of protocols (remember, protocol = set of rules) that are used to define how network communication should take place between hosts. While it isn't the only collection of protocols used to define network communication, it is the most often utilized one. As an example, TCP/IP includes the definition of how IP addresses and network masks work. |
