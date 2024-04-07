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


* TCP is a protocol used by hosts (computers or devices) to establish connections and exchange data reliably over a network.
* Routers, on the other hand, are networking devices that facilitate the routing of data packets between different networks.

**IP ADDRESSES**


IP addresses are numerical labels assigned to devices connected to a network to facilitate communication and identification. There are, in fact, two different types of IP addresses: IPv4 and IPv6

In an IPv4 address, a total of four 8-bit numbers are used to define the address. These numbers range from 0 to 255 and are separated by dots. Each of these numbers is called an octet.

Let's take the IPv4 address 192.168.1.1 as an example. In binary, each of the four numbers (192, 168, 1, and 1) is represented as 8 bits:
* 192 is 11000000
* 168 is 10101000
* 1 is 00000001
* 1 is 00000001

While it seems like there should be plenty of IP addresses to go around, various factors have led to a problem: the Internet started running out of IP addresses.

This issue encouraged the development of IPv6. IPv6 was officially created in 1998. In an IPv6 network, the addresses are much larger, 128-bit addresses that look like this:
2001:0db8:85a3:0042:1000:8a2e:0370:7334

It is important to note that the difference between IPv4 and IPv6 isn't just a larger address pool. IPv6 has many other advanced features that address some of the limitations of IPv4, including better speed, more advanced package management, and more efficient data transportation. However, the majority of network-attached devices in the world still use IPv4 (something like 98-99% of all devices).

There are primarily two reasons why the world hasn't embraced the superior technology of IPv6:

* NAT: Invented to overcome the possibility of running out of IP addresses in an IPv4 environment, Net Address Translation (NAT) used a technique to provide more hosts access to the Internet. In a nutshell, a group of hosts is placed into a private network with no direct access to the Internet; a special router provides Internet access, and only this one router needs an IP address to communicate on the Internet. In other words, a group of hosts shares a single IP address, meaning a lot more computers can attach to the Internet. This feature means the need to move to IPv6 is less critical than before the invention of NAT.
* Porting: Porting is switching over from one technology to another. IPv6 has a lot of great new features, but all of the hosts need to be able to utilize these features. Getting everyone on the Internet (or even just some) to make these changes poses a challenge.


### NETWORK INTERFACE CONFIGURATION

To make changes to a network interface, the widely accepted method involves taking the interface down, making the desired changes to the configuration file, and then bringing the interface back up. This can be achieved using commands such as `ifdown eth0` to take the interface down and `ifup eth0` to bring it back up.

Alternatively, a less specific method involves restarting the system’s networking entirely with a command like `systemctl network restart`. However, this action takes down all interfaces, re-reads all related configuration files, and then restarts the networking for the entire system. It's important to note that restarting the network service can disrupt more than just the single interface being modified, so it's advisable to use the most limited and specific commands to restart the interface whenever possible.

**CHANGING IP ADDRESS**

Changing the IP address of a network interface in Linux involves deactivating the interface, configuring the new IP address, and then activating the interface again. Keep in mind that you might need administrative privileges to execute these commands which means they must be run under the root access. Examples: 

`sudo ifconfig enp0s1 down` =  This command is used to deactivate or shut down a network interface named enp0s1 in a Linux system.

`sudo ip link set enp0s1 down`  = This command is also used to deactivate or shut down a network interface named enp0s1 in a Linux system.

`ifconfig enp0s1 192.168.0.111/24 up`: The command is used to manually configure the network interface enp0s1 with the IPv4 address 192.168.0.111 and a subnet mask of 255.255.255.0 (or /24). Additionally, the up keyword is used to activate or enable the network interface.

`ip address del 192.168.0.111/24 dev enp0s1` = This command is used to remove the current IP address.

`ip address add 192.168.0.112/24 dev enp0s1` =  This command is used to add an additional IP address to the network interface enp0s1 on a Linux system. The specified IP address is 192.168.0.112 with a subnet mask of 255.255.255.0 (or /24 in CIDR notation). 

**CHANGING THE DEFAULT GATEWAY**

Changing the default gateway in Linux involves modifying the routing table to specify a new gateway IP address. Examples:

`route -n` or `ip a route show` = These commands are used to show the gateway IP. 

`route del default gw 192.168.0.1` = The command is used to delete the current default gateway entry from the routing table in a Linux system.

`route add default gw 192.168.0.2` = The below command is used to add a new default gateway entry to the routing table in a Linux system. 

The above route commands will change the default route gateway IP using the `ifconfig` pattern.

`ip route del default` = This command deletes the existing default route from the routing table.

`ip route add default via 192.168.0.2 dev enp0s1`: This command adds a new default route to the routing table, specifying 192.168.0.2 as the gateway and enp0s1 as the network interface through which packets will be sent.

**CHANGING MAC ADDRESS**

Changing the MAC (Media Access Control) address of a network interface is a useful technique in networking for various reasons, including security and privacy. 

To change the MAC address, the first step is to disable the network interface in `ifconfig`. 

`ifconfig enp0s1 down` = This command as earlier mentioned is used to deactivate or shut down a network interface named enp0s1 in a Linux system. 

`ifconfig enp0s1 hw ether “new MAC address”` = This command is used to change the MAC (Media Access Control) address of a network interface named enp0s1 in a Linux system.
  - `hw ether`: This part of the command specifies that you are going to modify the hardware (MAC) address of the network interface.
  - `"new MAC address"`: This should be replaced with the new MAC address you want to assign to the network interface enp0s1. Ensure that the MAC address you specify is in the correct format, typically six pairs of hexadecimal digits separated by colons or hyphens (e.g., 00:11:22:33:44:55).

`ifconfig enp0s1 up` = This command is used to activate or enable a network interface named enp0s1 in a Linux system.

**SETTING UP STATIC IP ON UBUNTU (netplan)**

Laptops and Desktops have their IP addresses dynamically assigned by the DHCP server which  in most cases is the router. However, a server required a static configuration to avoid the single point of failure problem of using a DHCP server. 

Netplan is a utility for configuring networking on Linux systems. It has become the default network configuration tool for many Linux distributions that use the systemd init system.
Netplan configurations are written in YAML (Yet Another Markup Language), which aims to be human-readable and easy to understand located in /etc/netplan
Netplan renders backend service to control network interfaces on ubuntu based systems. 

An IP address, or Internet Protocol address, is a numerical label assigned to each device participating in a computer network that uses the Internet Protocol for communication. IP addresses serve two primary purposes: host or network interface identification and location addressing.

DNS, or Domain Name System, is a hierarchical and distributed naming system for computers, services, or other resources connected to the Internet or a private network. DNS translates human-readable domain names into IP addresses, which are used to locate and identify devices on a network. This process is essential for internet communication, as it allows users to access websites, send emails, and perform various online activities using memorable domain names instead of numerical IP addresses.
