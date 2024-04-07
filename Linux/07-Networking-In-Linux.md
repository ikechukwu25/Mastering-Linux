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

##### IP ADDRESSES

An IP address, or Internet Protocol address, is a numerical label assigned to each device participating in a computer network that uses the Internet Protocol for communication. IP addresses serve two primary purposes: host or network interface identification and location addressing. There are, in fact, two different types of IP addresses: IPv4 and IPv6

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

##### CHANGING IP ADDRESS

Changing the IP address of a network interface in Linux involves deactivating the interface, configuring the new IP address, and then activating the interface again. Keep in mind that you might need administrative privileges to execute these commands which means they must be run under the root access. Examples: 

`sudo ifconfig enp0s1 down` =  This command is used to deactivate or shut down a network interface named enp0s1 in a Linux system.

`sudo ip link set enp0s1 down`  = This command is also used to deactivate or shut down a network interface named enp0s1 in a Linux system.

`ifconfig enp0s1 192.168.0.111/24 up`: The command is used to manually configure the network interface enp0s1 with the IPv4 address 192.168.0.111 and a subnet mask of 255.255.255.0 (or /24). Additionally, the up keyword is used to activate or enable the network interface.

`ip address del 192.168.0.111/24 dev enp0s1` = This command is used to remove the current IP address.

`ip address add 192.168.0.112/24 dev enp0s1` =  This command is used to add an additional IP address to the network interface enp0s1 on a Linux system. The specified IP address is 192.168.0.112 with a subnet mask of 255.255.255.0 (or /24 in CIDR notation). 

##### CHANGING THE DEFAULT GATEWAY

Changing the default gateway in Linux involves modifying the routing table to specify a new gateway IP address. Examples:

`route -n` or `ip a route show` = These commands are used to show the gateway IP. 

`route del default gw 192.168.0.1` = The command is used to delete the current default gateway entry from the routing table in a Linux system.

`route add default gw 192.168.0.2` = The below command is used to add a new default gateway entry to the routing table in a Linux system. 

The above route commands will change the default route gateway IP using the `ifconfig` pattern.

`ip route del default` = This command deletes the existing default route from the routing table.

`ip route add default via 192.168.0.2 dev enp0s1`: This command adds a new default route to the routing table, specifying 192.168.0.2 as the gateway and enp0s1 as the network interface through which packets will be sent.

##### CHANGING MAC ADDRESS

Changing the MAC (Media Access Control) address of a network interface is a useful technique in networking for various reasons, including security and privacy. 

To change the MAC address, the first step is to disable the network interface in `ifconfig`. 

`ifconfig enp0s1 down` = This command as earlier mentioned is used to deactivate or shut down a network interface named enp0s1 in a Linux system. 

`ifconfig enp0s1 hw ether “new MAC address”` = This command is used to change the MAC (Media Access Control) address of a network interface named enp0s1 in a Linux system.
  - `hw ether`: This part of the command specifies that you are going to modify the hardware (MAC) address of the network interface.
  - `"new MAC address"`: This should be replaced with the new MAC address you want to assign to the network interface enp0s1. Ensure that the MAC address you specify is in the correct format, typically six pairs of hexadecimal digits separated by colons or hyphens (e.g., 00:11:22:33:44:55).

`ifconfig enp0s1 up` = This command is used to activate or enable a network interface named enp0s1 in a Linux system.



##### DNS 

DNS, or Domain Name System, is a hierarchical and distributed naming system for computers, services, or other resources connected to the Internet or a private network. DNS translates human-readable domain names into IP addresses, which are used to locate and identify devices on a network. This process is essential for internet communication, as it allows users to access websites, send emails, and perform various online activities using memorable domain names instead of numerical IP addresses.

**DNS Resolution:**
* When you enter a domain name in your web browser, your device sends a DNS query to a DNS resolver.
* The DNS resolver checks its cache to see if it already knows the corresponding IP address for the requested domain. If not, it forwards the request to higher-level DNS servers.
* The DNS query goes through a series of DNS servers, typically starting with the local resolver, then to the authoritative DNS server for the top-level domain (TLD), and finally to the authoritative DNS server for the specific domain.
* The authoritative DNS server for the domain provides the IP address associated with the requested domain name.
* The DNS resolver caches the IP address for future use, and your device uses this address to connect to the desired server.
  - DNS Resolver:
    * Resides on your device or on your ISP's server.
    * Responsible for initiating and handling DNS queries.
  - DNS Caching:
    * DNS resolvers cache IP addresses to reduce the time and resources needed for subsequent queries.
  
**DHCP (Dynamic Host Configuration Protocol):**
* DHCP is a network protocol used to dynamically assign IP addresses and other network configuration parameters to devices on a network. Using a different service provider can potentially change the DNS servers that your devices use to resolve domain names. Typically, when you connect to an internet service provider (ISP), they assign DNS servers automatically to your device through DHCP (Dynamic Host Configuration Protocol) or another configuration method.
* When a device joins a network, it typically sends out a DHCP request broadcast message.
* A DHCP server on the network responds to this request and provides the device with an IP address, subnet mask, default gateway, DNS server addresses, and other network configuration information.

**Integration of DNS and DHCP:**
* When a device receives network configuration information from a DHCP server, it often includes the IP address(es) of one or more DNS servers.
    * These DNS servers are the ones the device will use to perform DNS resolution for domain names.
* By providing DNS server information during the DHCP process, devices on the network can immediately start resolving domain names into IP addresses without any additional configuration.

**Nameserver Setting:**
* The nameserver setting is typically configured in the /etc/resolv.conf file on Linux systems.
* This setting specifies the IP address(es) of the DNS server(s) that the system should use for DNS resolution. The nameserver setting is often set to the IP address of the DNS server.
* For example, a line like nameserver 192.168.1.2 in the /etc/resolv.conf file indicates that the system should use the DNS server at IP address 192.168.1.2 for DNS resolution. 

The following example uses the host command, which works with DNS to associate a hostname with an IP address. Note that the example server is associated with the IP address 192.168.1.2 by the DNS server:

`ikechukwu@ubuntu-22-04-3:~$ host example.com`                       
`example.com has address 192.168.1.2`

The `host command` is a utility used in Unix-like operating systems (including Linux) for performing DNS lookups and querying DNS servers to retrieve information about domain names and IP addresses.

Remember that the address of the DNS server is stored in the /etc/resolv.conf file. 

Name resolution on a Linux host is accomplished by 3 critical files: the /etc/hosts, /etc/resolv.conf and /etc/nsswitch.conf files. Together, they describe the location of name service information, the order in which to check resources, and where to go for that information.

When you run `ifconfig`, the lo device is referred to as the loopback device. It is a special network device used by the system when sending network-based data to itself.

| Files | Explanation |
|--------|--------|
| /etc/hosts |	In the /etc/hosts file, your computer keeps a list of names (hostnames) and their corresponding addresses (IP addresses) of other computers or devices on the internet. So, when your computer needs to communicate with another computer, it can quickly look up the address of that computer in its /etc/hosts file. </br></br> `sysadmin@localhost:~$ cat /etc/hosts`</br>`127.0.0.1       localhost` | 
| /etc/resolv.conf |	This file contains the IP addresses of the name servers the system should consult in any attempt to resolve names to IP addresses. These servers are often DNS servers. It also can contain additional keywords and values that can affect the resolution process. </br></br> It's a file stored on your computer (specifically in the /etc directory) that contains important information about how your computer finds the IP addresses of websites when you type in their names (like www.example.com).</br></br> Each line in the file contains the IP address of one of these DNS servers that your computer should ask when it needs to find the IP address of a website. </br></br> `sysadmin@localhost:~$ cat /etc/resolv.conf`</br> `nameserver 127.0.0.11` |
| /etc/nsswitch.conf |	This file can be used to modify where hostname lookups occur. It contains a particular entry that describes in what order name resolution sources are consulted.</br></br> It stands for "Name Service Switch Configuration" and determines how the system performs various name resolution tasks, including hostname lookups.</br></br> Hostname lookups involve translating human-readable hostnames (like "www.example.com") into IP addresses (like "192.168.1.1") that computers understand. </br></br> The key entry in /etc/nsswitch.conf that controls hostname lookups is typically the hosts entry.</br></br> `sysadmin@localhost:~$ cat /etc/nsswitch.conf` </br> `# /etc/nsswitch.conf`</br> `#` </br></br> `Output Omitted...`</br></br> `hosts:          files dns`</br></br> `Output Omitted...`</br></br> The /etc/hosts file is searched first, the DNS server second: </br> hosts: files dns </br>The DNS server would be searched first, local files second:</br>hosts: dns files |
	
How Does It Work? (/etc/resolv.conf)
* When you type a website's name into your browser, your computer looks at /etc/resolv.conf to find out which DNS servers it should ask.
* Then, your computer sends a message to one of those DNS servers, asking, "Hey, what's the IP address of www.example.com?"
* The DNS server checks its big phonebook, finds the IP address for www.example.com, and sends it back to your computer.
* Finally, armed with the IP address, your computer connects to the website you want to visit.


How It Works: (/etc/nsswitch.conf)
* When you try to access a website or connect to a server by its hostname, your system consults the host entry in /etc/nsswitch.conf.
* Based on the order specified in this file, your system checks the designated sources (such as files or DNS servers) one by one until it finds a matching hostname-to-IP address mapping.
* Once a match is found, your system uses the corresponding IP address to establish the connection or access the resource you requested.


1. First, the /etc/nsswitch.conf file is consulted: </br>
hosts:	files dns</br>
This line indicates that the system should consult local files first in an attempt to resolve hostnames, which means that tells your system to check its local files first when trying to find the IP address of a hostname. This means it will look in the /etc/hosts file to see if it can find a match for the hostname you're trying to reach.
2. Second, the system will consult the /etc/hosts file to attempt to resolve the name. If the name matches an entry in /etc/hosts, it is resolved. It will not failover (or continue) to the DNS option, even if the resolution is inaccurate. This can occur if the entry in /etc/hosts points to a non-assigned IP address.
3. Third, if the local /etc/hosts file doesn’t result in a match, the system will use the configured DNS server entries contained in the /etc/resolv.conf file to attempt to resolve the name. The /etc/resolv.conf file should contain at least two entries for name servers, such as the example file below:</br></br>
nameserver 10.0.2.3</br>
nameserver 10.0.2.4</br></br>
The DNS resolution system will use the first name server for an attempted lookup of the name. If that is unavailable, or a timeout period is reached, the second server will then be queried for the name resolution. If a match is found, it is returned to the system and used for initiating a connection and is also placed in the DNS cache for a configurable time period. 


##### SETTING UP STATIC IP ON UBUNTU (netplan)

Laptops and Desktops have their IP addresses dynamically assigned by the DHCP server which in most cases is the router. However, a server requires a static configuration to avoid the single point of failure problem of using a DHCP server. 

Netplan is a utility for configuring networking on Linux systems. It has become the default network configuration tool for many Linux distributions that use the systemd init system.

Netplan configurations are written in YAML (Yet Another Markup Language), which aims to be human-readable and easy to understand located in /etc/netplan
Netplan renders backend service to control network interfaces on ubuntu based systems. 

When configuring a static IP address on a device, understanding the concept of subnetting and the role of the netmask is crucial. In the context of static IP configuration, the netmask determines the size and boundaries of the network to which the device belongs. It helps the device identify whether another device it wants to communicate with is within the same network or in a different network.

When a device wants to communicate with another device, it checks whether the destination IP address is in the same "section" (or network) as itself. The netmask helps the device determine which part of the IP address identifies the network and which part identifies the specific device within that network. It's a way to organize and manage communication on a network.

For example, consider a scenario where you're setting a static IP address on a device with the IP address 192.168.1.5 and a netmask of 255.255.255.0 (or /24 in CIDR notation). In this case, the netmask 255.255.255.0 indicates that the first three octets of the IP address (192.168.1) represent the network, while the last octet (5) represents the specific device within that network.

Now, if another device has the IP address 192.168.1.10 with the same netmask 255.255.255.0, both devices are in the same network (192.168.1) because their network portions are identical. Therefore, they can communicate directly with each other without needing a router.

However, if the netmask were different, such as 255.255.0.0 (or /16), it would indicate a larger network, allowing devices with IP addresses like 192.168.1.5 and 192.168.2.10 to be in the same network. Conversely, if the netmask were more restrictive, such as 255.255.255.128 (or /25), it would result in smaller subnetworks within the 192.168.1.x range, affecting which devices can directly communicate with each other.

Some important network configuration tools include - NetworkManager and systemd-networkd. These tools enable users to configure, manage, and maintain network connections on Linux systems.

NetworkManager is a network management service commonly found in Linux distributions, which offers a graphical user interface (GUI) for managing network connections. This GUI provides users with a visual way to configure and manage network settings such as Wi-Fi connections, Ethernet connections, VPNs, and more.

"systemd-networkd" is another network management service available in Linux distributions, but unlike NetworkManager, it does not have a built-in graphical user interface. Instead, systemd-networkd is designed to be controlled primarily through configuration files and command-line tools. It focuses on providing a lightweight and efficient solution for managing network connections, particularly in server environments or headless systems where GUI tools may not be available or necessary.

How to configure the network server if there is no GUI (Network Manager) available using the systemd-networkd renderer

1. Stop the network manager - The network interface can be managed by either of both and not by both. - `systemctl stop NetworkManager`
2. Disable network manager - `systemctl disable NetworkManager`
3. Confirm if the NetworkManager will start at boot time. - `systemctl is-enabled NetworkManager`
4. Create a .yaml file in /etc/netplan and remove the Network Manager’s yaml file in /etc/netplan as it could interfere with the static configuration; 
`vim /etc/netplan/01-netconfig.yaml`</br>
`network:`</br>
`  version: 2`</br>
`  renderer: networkd`</br>
`  ethernets:`</br>
`    enp0s3:`</br>
`      dhcp4: false`</br>
`      addresses:`</br>
`        - 192.168.0.20/24`</br>
`      gateway4: "192.168.0.1"`</br>
`      nameservers:`</br>
`        addresses:`</br>
`          - "8.8.8.8"`</br>
`          - "8.8.4.4"` </br>
This example configures the enp0s3 interface with a static IP address, gateway, and DNS servers.
5. Validate the YAML file:
You can use a YAML validator such as [yamllint](https://www.yamllint.com/) to ensure your configuration file has no syntax errors.
6. To save the changes on the /etc/netplan file created, run as root - netplan apply
7. Run `ifconfig` to verify the changes has taken place on the IP and run route -n to confirm the changes has taken effect on the default gateway. 


