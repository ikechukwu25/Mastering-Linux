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

To obtain specific information about a particular interface, you can use commands like `ifconfig <interface-name>` or `ip address show dev <interface-name>`.
For example, `ifconfig enp0s3` or `ip address show dev enp0s3`

`route`

The `route` command is primarily used to display and manipulate the IP routing table on Linux systems, which includes information about network routes and gateways. It provides details about how network packets should be forwarded to their destinations.

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

`ifconfig enp0s1 192.168.0.111/24 up` = The command is used to manually configure the network interface enp0s1 with the IPv4 address 192.168.0.111 and a subnet mask of 255.255.255.0 (or /24). Additionally, the up keyword is used to activate or enable the network interface.

`ip address del 192.168.0.111/24 dev enp0s1` = This command is used to remove the current IP address.

`ip address add 192.168.0.112/24 dev enp0s1` =  This command is used to add an additional IP address to the network interface enp0s1 on a Linux system. The specified IP address is 192.168.0.112 with a subnet mask of 255.255.255.0 (or /24 in CIDR notation). 

##### CHANGING THE DEFAULT GATEWAY

Changing the default gateway in Linux involves modifying the routing table to specify a new gateway IP address. Examples:

`route -n` or `ip a route show` = These commands are used to show the gateway IP. 

`route del default gw 192.168.0.1` = The command is used to delete the current default gateway entry from the routing table in a Linux system.

`route add default gw 192.168.0.2` = The below command is used to add a new default gateway entry to the routing table in a Linux system. 

The above route commands will change the default route gateway IP using the `ifconfig` pattern.

`ip route del default` = This command deletes the existing default route from the routing table.

`ip route add default via 192.168.0.2 dev enp0s1` = This command adds a new default route to the routing table, specifying 192.168.0.2 as the gateway and enp0s1 as the network interface through which packets will be sent.


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

The following example uses the `host` command, which works with DNS to associate a hostname with an IP address. Note that the example server is associated with the IP address 192.168.1.2 by the DNS server:

`ikechukwu@ubuntu-22-04-3:~$ host example.com`                       
`example.com has address 192.168.1.2`

The `host` command is a utility used in Unix-like operating systems (including Linux) for performing DNS lookups and querying DNS servers to retrieve information about domain names and IP addresses.

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

The `dig` and `host` commands are both used for DNS-related tasks but have slightly different functionalities and use cases. Collectively, these commands are used for DNS querying, resolving hostnames to IP addresses, and retrieving detailed DNS information about a domain. </br></br>


**THE `dig` COMMAND**

There may be times when you need to test the functionality of the DNS server that your host is using. One way of doing this is to use the `dig` command, which performs queries on the DNS server to determine if the information needed is available on the server.

In the following example, the `dig` command is used to determine the IP address of the example.com host:

`root@ubuntu-22-04-3:~# dig example.com`

If the DNS server doesn't have the requested information, it is configured to ask other DNS servers. If none of them have the requested information, an error message displays.

To resolve a fully-qualified domain name (FQDN), you simply provide the domain name as an argument to the `dig` command. 

`dig example.com`

And you can use the `dig` command to resolve the IP address 192.168.1.2 to a hostname:

`dig -x 192.168.1.2` = The `-x` option tells dig to perform a reverse DNS lookup.</br></br> 


**THE `host` COMMAND**

In its simplest form, the `host` command works with DNS to associate a hostname with an IP address.

`root@ubuntu-22-04-3:~# host example.com`   

The `host` command can also be used in reverse if an IP address is known, but the domain name is not.

`root@ubuntu-22-04-3:~# host 192.168.1.2`

A comprehensive list of DNS information regarding example.com can be found using the `-a` all option:

`root@ubuntu-22-04-3:~# host -a example.com`      

Sometimes, a system may be configured to not respond to ping requests. Therefore, the lack of a response to a `ping` command does not mean a system is not connected to a network. A quick response to a `ping` command does indicate, however, that a system is connected to a network.


### SETTING UP STATIC IP ON UBUNTU (netplan)

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


### TESTING AND TROUBLESHOOTING NETWORK CONNECTIVITY

Ping is a network utility tool that is commonly used to test the reachability of a host on an Internet Protocol (IP) network and to measure the round-trip time for messages sent from the originating host to a destination computer. 

ICMP (Internet Control Message Protocol): Ping uses ICMP Echo Request and Echo Reply messages to check if a remote host is reachable and measure the round-trip time. ICMP is a network layer protocol and is part of the Internet Protocol suite.


When you use the `ping` command, it can perform a reverse DNS lookup on the IP addresses of the hosts it is trying to reach. This means that, in addition to sending ICMP Echo Request messages to check the reachability of a host, ping can also try to determine the domain name associated with the IP address.

To prevent this, use the `-n` option. 

64 bytes from website-content-cache-1.ps5.canonical.com (185.125.190.20): icmp_seq=7 ttl=48 time=242 ms 

* 64 bytes from website-content-cache-1.ps5.canonical.com (185.125.190.20):
    * This part indicates that the response is received from the IP address 185.125.190.20.
    * website-content-cache-1.ps5.canonical.com is the domain name associated with the IP address, determined through a reverse DNS lookup.
* icmp_seq=7 This shows the sequence number of the ICMP Echo Request and Echo Reply pair. In this case, it's the 7th sequence.
* ttl=48 This is the number of routers between the source and the destination. The TTL value of an IP packet represents the maximum number of IP routers that the packet can go through before being thrown away. It is decremented by each router the packet passes through. The TTL here is 48.
* time=242 ms This is the round-trip time for the ICMP Echo Request and Echo Reply, measured in milliseconds. It represents the time taken for the packet to travel from the source to the destination and back. In this case, it's 242 milliseconds.

- `ping -i new interval time` = to change interval for output. Only the admin can change it below 0.2
- `ping -t 5` = shows the 5th router towards the destination.

To Troubleshoot,
1. Ping the default gateway of the LAN - `route -n` or `ip route show` to get the default gateway, ping it. If it doesn’t work, either you’re not authenticated, or you don’t have the correct IP, or the route is not correctly configured. 
2. Ping the public IP address on the internet like Google DNS -8.8.8.8. If it doesn’t work, means there is an internet connectivity issue.
3. Ping an internet DNS like google.com. if it’s not working you have a DNS issue. 


 ### USING SSH

SSH is a network protocol used by sysadmins to securely configure a remote system over an insecure network connection. SSH provides a secure channel over an unsecured network by encrypting the communication between the client and the server.

To install SSH (OpenSSH server and client) on your system, you can use the following commands:

- `sudo apt update && sudo apt install openssh-server openssh-client`: </br></br>
- `sudo apt update` = This part of the command updates the package list</br>
- `sudo apt install openssh-server openssh-client` = This command will install the OpenSSH server and client packages. 

SSH Server:</br>
    * The SSH server is the program or daemon running on a remote machine that listens for incoming SSH connections.</br>
    * It allows remote users to connect securely, execute commands, and transfer files. </br>
SSH Client:</br>
    * The SSH client is the program or tool used by a user to connect to a remote system securely.</br>
    * It allows users to log in to a remote machine, execute commands on the remote system, and transfer files securely.

- `ssh username@IP address` OR `ssh -l username IP address` = This command is used to ssh into another machine.
- `ssh -p username IP` = This command will change the port number. 


### TROUBLESHOOTING SSH

If you cannot connect to the remote server, 
- The first thing is to check that the ssh daemon is running on the machine by running - `systemctl status ssh`
- Try restarting the service by running - `systemctl restart ssh`
- If on the client part you get the below error response when trying to connect the authenticator, you should double-check to confirm you’re connecting to the right server. Also, you can access the host keys via `cat .ssh/known_hosts` file and remove the server’s key `vi .ssh/known_hosts`. When connecting to the server, the new messages about the correct server will be displayed. 

￼<img width="862" alt="Add correct host key in homeandrei sshknown hosts to get rid of this message" src="https://github.com/ikechukwu25/Mastering-Linux/assets/64879420/1667126f-4436-4669-ac0c-0fd0991a993d">

- If the ssh connection is still not working check if the port 22 on which the server license is opened. From the client, scan port 22 using a command like `telnet` or `nmap` (install telnet first - `sudo apt install telnet`). Afterwards, run `telnet IP port number` (22) to connect to the server. Or install `nmap` and run `nmap -p 22 IP`
- Check if there is a firewall that is dropping the packets by running sudo `iptables -vnL`. If there is a firewall issue, then Ubuntu could have "ufw". To configure the ufw file to allow incoming ssh connections, use `sudo ufw allow ssh`
- Run `ssh -v username@IP address` = This is helpful with debugging authentication and configuration problems. Multiple `-v` options are used to increase the verbosity. 
- If the problem still persists, check the server log file - /var/log/auth.log.


### FIREWALL RULES IN LINUX

A Linux firewall is your computer's security guard, deciding what information can come in and go out. It protects your computer from unwanted visitors and ensures a safe and controlled flow of data.

Firewall rules in a Linux system define how incoming and outgoing network traffic should be handled. They act as a set of instructions that the system's firewall follows to determine whether to allow or deny specific packets based on predefined criteria. In Linux, the firewall rules are typically managed using tools like `iptables`, `nftables`, or user-friendly frontends like Uncomplicated Firewall (UFW).

`ufw` (Uncomplicated Firewall) and `iptables` are both tools used for managing firewall rules on Linux systems. `ufw` is designed to simplify the process of configuring `iptables` and is often considered more user-friendly, especially for users who are not familiar with the complexities of `iptables`.

`iptables` is a command-line utility for configuring the IP packet filter rules of the Linux kernel firewall. `ufw` is a user-friendly command-line interface for managing `iptables`. It is designed to make firewall configuration more accessible.

- `ufw status verbose` = Used to see status of ufw
- `sudo ufw app list` = List all application profiles available.

The .ssh/known_hosts file is a file used by SSH (Secure Shell) to store information about host keys of remote servers. When you connect to a remote server for the first time, its public key is added to the known_hosts file on your local machine. This file helps to verify the authenticity of the remote server during subsequent connections.

In Linux, SSH (Secure Shell) servers use specific ports for communication. The default port for SSH is 22. However, there might be scenarios where you want to change the default SSH port for security reasons.

To permit ssh access only from two IP addresses or networks, the following iptables rules are required;

- `iptables -A INPUT -p tcp --dport 22 -s 192.168.64.1 -j ACCEPT` = Allow SSH connections from the IP address 192.168.64.1.
- `iptables -A INPUT -p tcp --dport 22 -s 192.168.64.1 -j ACCEPT` = Allow SSH connections from another IP address or network.
- `iptables -A INPUT -p tcp --dport 22 -j DROP` = Drop (block) all other SSH connections.

Only SSH connections coming from these two IP addresses will be permitted. 
If you want to allow an entire network, use the network address instead of the IP address


### SECURING THE OPENSSH SERVER (sshd)

The server configuration file is located in /etc/ssh/sshd_config. To change anything about the server, you have to edit the file and restart the server. 
The client configuration file is located in /etc/ssh/ssh_config.
Open `man sshd_config` and search for each option from the sshd_config file.

Recommendations on securing the SSH

- By default, the ssh daemon is listening for incoming connections on port 22. You can change the port and don’t forget to make the required changes to the firewall rules.  
- Prohibit direct root login via SSH to minimize the risk of unauthorized access. - Change PermitRootLogin to no
- Disable password authentication entirely and enable only public key authentication. If you need to allow password authentication, enforce strong password policies.
- Limit the user ssh access as by default all users can login - AllowUsers username username username 
- Filter SSH access at the firewall level - To filter SSH access at the firewall level, you can use a firewall management tool like ufw (Uncomplicated Firewall) on Ubuntu.
	- `sudo apt update && sudo apt install ufw` = Install ufw if it's not already installed.
	- `sudo ufw allow ssh` = Allow SSH connections.
	- `sudo ufw default deny incoming` = Deny incoming connections on other ports (if needed).
	- `sudo ufw enable` = Enable the firewall.
	- `sudo ufw status` = Verify the firewall status.
- Use ssh protocol version 2: To see the version, run `ssh -v username@hostname`.  On the server side, you can often configure the accepted SSH protocol versions in the SSH server configuration file (e.g., /etc/ssh/sshd_config). Look for a line like Protocol 2 which specifies the protocol version. If it's set to 2, it indicates SSH-2. You can change it to 1 to allow SSH-1 or 2 to allow both SSH-1 and SSH-2 (though SSH-1 is strongly discouraged for security reasons).
- Configure an idle timeout interval - Automatically disconnect idle sessions after a certain period. - ClientAliveInterval - The ClientAliveInterval option in the SSH server configuration (sshd_config file) specifies the time (in seconds) that the server will wait before sending a "null packet" to the client to keep the connection alive. This is useful to prevent network devices from closing idle SSH connections due to inactivity. If set at 300 seconds, once elapsed, the user will be automatically logged out.


### COPYING FILES OVER THE NETWORK (scp)

`scp` (Secure Copy Protocol) is a command-line utility used for securely copying files between hosts on a network. Can be used in 3 ways - Copy from a remote server to the computer, from the computer to a remote server, or from one remote server to another tremor server.

- Copying a local file to a remote destination.
	- `scp a.txt john@80.0.0.1:~`= The command will copy the file a.txt from the current directory on your local machine to the home directory (~) of the user john on the remote server with the IP address 80.0.0.1.
	- `scp -P 2288 a.txt john@80.0.0.1:~` = The command will copy the file a.txt from your local machine to the home directory (~) of the user john on the remote server with the IP address 80.0.0.1, using port 2288.
	- `scp -P 22 ip.txt ikechukwu@192.168.64.2:~/ip_conf.txt` = The command will copy the file named ip.txt from the current directory on your local machine to the home directory (~/) of the user ikechukwu on the remote server with the IP address 192.168.64.2, using the default SSH port 22.
	- `scp -rp -P 22 mydir1 ikechukwu@192.168.64.2:~` (-r = recursive, -p = preserves the modification and access time)  #used to copy a directory 
- Copying a file from the remote server to the local client.
	- `scp ikechukwu@192.168.64.2:/etc/passwd  /home/ikechukwu/Desktop` = This command copies the /etc/passwd file from the remote server located at 192.168.64.2 under the user ikechukwu to the local directory /home/ikechukwu/Desktop. 
	- `scp -r ikechukwu@192.168.64.2:~/Desktop  /home/ikechukwu/Desktop` = This command recursively copies the contents of the Desktop directory from the remote server located at 192.168.64.2 under the user ikechukwu to the local directory. It is used to copy a directory 
- `scp user1@IP1:/path_to_the_source_file user2@IP2:path_to_the_destination_directory` = This command copies a file from a source location on one remote server to a destination directory on another remote server. 


## SFTP

SFTP, or Secure File Transfer Protocol, is a secure and encrypted file transfer protocol that is part of the SSH (Secure Shell) suite of network protocols. SFTP provides a secure way to transfer files between computers over a network. It has a GUI eg. FileZilla


### SYNCHRONIZING FILES AND DIRECTORIES USING (rsync)

`rsync` is a powerful command-line utility for synchronizing files and directories between two locations on a Unix-like operating system. It is widely used for efficient and incremental file transfers, making it a popular choice for backups, mirroring, and remote file synchronization.

N/B: The user that runs the rsync command must have read permission on the source location and write permission on the destination directory location. 

- `rsync -av /etc/ ./etc-backup`: The source directory with a trailing slash copies the entire source directory (/etc), including its contents, to the destination directory (./etc-backup)
- `rsync -av /etc ./etc-backup`: The source directory without a trailing slash copies the contents of the source directory (/etc) to the destination directory (./etc-backup). The directory structure inside ./etc-backup will mirror the structure of /etc, but the source directory itself (/etc) is not copied.
- `rsync -av --delete /etc/ ./etc-backup` = This command is used to sync deleted files too include the --delete option.

To exclude files when synchronising, run the following commands as described;
- Create a new file containing the names of the files and directories you wish to exclude. `vim exclude_files.txt`
- To synchronize the files from source_directory to destination_directory while excluding excluded_file.txt, you would run the following rsync command:
	- `rsync -av --exclude-from="/home/user/exclude_files.txt" /home/user/source_directory/ /home/user/destination_directory/` 
- To exclude a particular type of file = `rsync -av --exclude="*.txt" sourcedir destinationdir`


### USING RSYNC OVER THE NETWORK

When you want to backup or mirror your server configurations over the network. These commands illustrate how `rsync` can be used to backup or mirror server configurations over the network:

- `sudo rsync -av -e ssh /etc/ ikechukwu@192.168.64.2:~/etc-backup/` = This command synchronizes the contents of the /etc/ directory to the etc-backup directory on the remote server using SSH for secure communication.
- `sudo rsync -av —delete -e ssh /etc/ ikechukwu@192.168.64.2:~/etc-backup/` = This command is used to synch deleted items. Adding the `--delete` option ensures that any files or directories on the destination that do not exist in the source (/etc/ directory) are deleted.
- `sudo rsync -av —delete -e #ssh -p 22" /etc/ ikechukwu@192.168.64.2:~/etc-backup/` = By specifying the `-p` 22 option, the command instructs SSH to use port 22 for communication instead of the default port.
- `sudo rsync -av —delete -e ssh ikechukwu@192.168.64.2:~/etc/ ./etc-linux/` = This command synchronizes the contents of the /etc directory on the remote server to the etc-linux directory on the local machine.


### USING wget 

The wget command is a powerful tool for downloading files from the internet. Here are some common options and usage scenarios:

- `wget -P dir/ URL` = This command is used to download a file to a particular directory
- `wget --limit-rate=100k -P dir/ URL` = This option limits the download speed to 100 kilobytes per second (100k).
- `wget -c -P dir/ URL` = The -c option is used to resume a download.  

- To download multiple files (-i)
	- `vi images.txt`
	- Input links to the file = image.txt 
	- `wget -i images.txt`  
- To download large files in the background:
	- `wget -b URL &`
	- `tail -f logname`
	- `pkill wget`
- `nohup wget -b -i URL` = When you use `nohup` with a command like `wget`, it allows the command to continue running even after you log out or close the terminal. 
- `wget -mkEpnp URL` = The wget command with the options -mkEpnp is commonly used for recursive downloading of a website, including converting links for offline viewing. Let's break down the options:
	* `-m`: Enables mirroring. This option turns on recursion and time-stamping, sets infinite recursion depth, and removes the size limitations on downloaded files.
	* `-k`: Converts the links in the downloaded documents to make them suitable for offline viewing. This includes converting links to local copies, so you can browse the downloaded site without an internet connection.
	* `-E`: Appends the .html extension to HTML files without it. This is useful for making the downloaded pages easier to open in a browser.
	* `-p`: Downloads all necessary files for displaying any HTML page. This includes images, stylesheets, and other resources linked from the HTML files.
	* `-n`: Turns on timestamping, allowing `wget` to download only newer files if the local version is outdated.
	* `-P`: Specifies the directory prefix where all files and directories are saved. If not specified, files are saved in the current directory.


### CHECKING FOR LISTENING PORTS 

Checking for listening ports on a system is crucial for network administration and security monitoring. `netstat`, `ss`, and `lsof` are commonly used to display open ports on the current system or locate hosts. Here are several methods and tools commonly used for this purpose:

**The `netstat` command** (now “ss”)

The `netstat` command is a powerful tool that provides a large amount of network information. It can be used to display information about network connections as well as display the routing table similar to the `route` command. To display statistics regarding network traffic, use the `-i` option to the `netstat` command.

- `root@localhost:~# netstat -i`</br>                                                 
`Kernel Interface table`</br>                                                        
`Iface   MTU Met   RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg`</br>
`eth0       1500 0       137      0      4 0        12      0      0      0 BMRU`</br>
`lo        65536 0        18      0      0 0        18      0      0      0 LRU`

The most important statistics from the output above are the TX-OK and TX-ERR. A high percentage of TX-ERR may indicate a problem on the network, such as too much network traffic.

To use the `netstat` command to display routing information, use the `-r` option:

The `netstat` command is also commonly used to display open ports. A port is a unique number that is associated with a service provided by a host. If the port is open, then the service is available for other hosts.

To see a list of all currently open ports, use the following command:

- `root@ubuntu-22-04-3:~# netstat -tln`</br>
`Active Internet connections (only servers)`</br>
`Proto Recv-Q Send-Q Local Address           Foreign Address         State` </br>
`tcp        0      0 192.168.1.2:53          0.0.0.0:*               LISTEN`</br>
`tcp        0      0 127.0.0.1:53            0.0.0.0:*               LISTEN`</br>
`tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN`</br>
`tcp        0      0 127.0.0.1:953           0.0.0.0:*               LISTEN`</br>
`tcp6       0      0 :::53                   :::*                    LISTEN`</br>
`tcp6       0      0 :::22                  :::*                    LISTEN`</br>
`tcp6       0      0 ::1:953                 :::*                    LISTEN`

In the previous example, `-t` stands for TCP, `-l` stands for listening (which ports are listening), and `-n` stands for show numbers, not names.

Sometimes showing the names can be more useful. This can be achieved by dropping the `-n` option

This program is obsolete. The replacement for `netstat` is `ss`.</br> 
The replacement for `netstat -r` is `ip route`. </br>
The replacement for `netstat -i` is `ip -s link`. </br>
The replacement for `netstat -g` is `ip maddr`.

- `netstat -tupan` = This command shows all open ports. 

	- `-t` = shows TCP ports </br>
	- `-u` = shows UDP ports </br>
	- `-p` = Show the process ID and name associated with each socket. </br>
	- `-a` = Display all sockets (both listening and non-listening). </br>
	- `-n` =  Show numerical addresses and port numbers instead of resolving them to hostnames and services. 

`sudo netstat -tupan | grep :22 = searches for all port : 22` = This command searches for all port : 22 


**The `ss` Command**

The `ss` command is designed to show socket statistics and supports all the major packet and socket types. Meant to be a replacement for and to be similar in function to
the `netstat` command, it also shows a lot more information and has more features.

When you run `ss`, the output is very similar to the output of the `netstat` command with no options. The columns above are:

| Field | Description |
|-----|-----|
| Netid	| The socket type and transport protocol |
| State	| Connected or Unconnected, depending on protocol |
| Recv-Q	| Amount of data queued up for being processed having been received |
| Send-Q	| Amount of data queued up for being sent to another host |
| Local Address	| The address and port of the local host’s portion of the connection |
| Peer Address	| The address and port of the remote host’s portion of the connection |

The format of the output of the `ss` command can change dramatically, given the options specified, such as the use of the `-s` option, which displays mostly the types of sockets, statistics about their existence, and numbers of actual packets sent and received via each socket type.

**TCP**
Local Address: This is the local IP address and port number. In this case, it is "0.0.0.0:22." The IP address "0.0.0.0" means that the server is listening on all available network interfaces, and ":22" is the port number.
Foreign Address: For a listening socket, the foreign address is usually "0.0.0.0:*," indicating that it can accept connections from any remote IP address on any port.

**UDP**
Local Address: This is the local IP address and port number. In this case, ":::5353". The ":::" notation represents all available IPv6 addresses on the system, and "5353" is the port number.
Foreign Address: For a listening socket, the foreign address is usually ":::*," indicating that it can accept connections from any remote IPv6 address on any port.


**The `lsof` command**

- `lsof` (List Open Files) is a command-line utility used to display information about files and processes currently open or in use by the system.
- `sudo ls -u username` = This command lists files and processes that are currently open by the user. 
- `lsof -u ^ikechukwu` = The negation symbol can be used to see all files opened except a specific user.
- `lsof -iTCP -sTCP:LISTEN -nP` = This command is used to see files that have opened TCP ports (`iTCP sTCP:LISTEN` shows only the files that opened TCP ports which are in the listening state)
	* `-iTCP`: Specifies that the information should be related to the TCP (Internet protocol) family.
	* `-sTCP:LISTEN`: Filters the results to show only those connections in the LISTEN state (i.e., processes that are actively listening for incoming connections).
	* `-nP`: Prevents `lsof` from resolving hostnames (numeric output) and from converting port numbers to service names (numeric port output).
- `sudo lsof -iTCP:22 -sTCP:LISTEN -nP` = This command is used to identify which file has opened a specific port (e.g., port 22 in this example).


**The `telnet` command**

To check what ports are open in another system, scan the ports on that system using `telnet` command. For example; 

- `telnet IP Port number` - `telnet 192.168.64.1 22` = If the connection is successful, you'll typically see a blank screen or a message indicating that the connection has been established. If the connection fails, you may receive an error message indicating the reason for the failure.

To quit telnet, press "Ctrl + ]" and then type quit.


**The `nmap` command**

For professional port scanning, nmap is a widely used tool. Install it using `sudo apt install nmap` and use commands like `nmap -p 80 linux.com` to see the status of a specific port.
Please see for more information on the `nmap` command.
