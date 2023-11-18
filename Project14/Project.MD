# UNDERSTANDING IP ADDRESSES AND CIDR NOTATION

## Introduction: 
Understanding networking is a fundamental part of configuring complex environments on the internet. This has implications when trying to communicate between servers efficiently, developing secure network policies, and keeping your nodes organized.
In this project we are going to discuss some more specific concepts that are involved with designing or interacting with networked computers. Specifically, we will be covering network classes, subnets, and CIDR notation for grouping IP addresses.

## INTRODUCTION TO IP ADDRESSES
**Internet Protocol (IP)** is a set of governing rules for data packets, data format, or datagram sent through a local network or the internet. It is a connectionless and datagram-oriented protocol as it works on a dynamic computer network.

An IP works without a centralized monitor or directory and never relies on a node or link. Hence, each data packet must have the source and destination’s IP address and other key information to get delivered successfully.

**What is an IP Address:**
An Internet Protocol Address (IP address) refers to a unique address or numerical label designated for each device connected in a computer network using the Internet Protocol (IP) for communication.

Example of an IP address: 192.16.2.1, each number in the set can range from 0 to 255, so the full IP addessing range goes from 0.0.0.0 to 255.255.255.255. They are mathematically produced and alocated by Internet Assigned Numbers Authority (IANA) manages IP addresses globally, and 5 Regional Internet Registries (RIRs) manage them in designated regions and assign them to locat internet registeries like the end-users and internet Service Providers.

IP addresses identify a device on a local network or the internet and allow data to be transmitted between the devices, containing location information while making devices accessible for easy communication. IP addresses offer a great way of differentiating between different devices like computers, printers, websites, routers, etc.

An IP address is used for two purposes:
* Location finding
* Identifying host/network interface

## Types of IP Addresses
The below screenshot shows the different types of IP Address:
![Alt text](<Images/Types of IP Address.png>)

1. Public and Private
A business or individual having an internet service has IP addresses of two types: private and public. These IP addresses are based on the network location.

Private IP Address: It is used inside the computer network within your home or office. Every device (computer, smartphone, speakers, smart TV, etc.) connecting to your network consists of a private IP address assigned by your router.
As the usage of different devices is growing, the number of IP addresses at home grows with it. Hence, your router must find a way to detect these systems separately, which is why it generates unique private IP addresses for each of them, differentiating devices on your network. Devices outside the private network will not be able to access the private IP addresses.

Public IP address: It is used outside your home or office computer network. Each device connected to the public network or internet will have its IP address assigned by the Internet Service Provider (ISP). ISPs have a wide range of IP addresses for customers, and they allocate a public IP address to your router.
External devices use public IP addresses to find your device over the internet. A public IP address is of two types: static and dynamic.

#2. Static and Dynamic
Static IP addresses: They are consistent and don’t change regularly or automatically. Once the ISP assigns it, the IP stays the same.
Every business or individual does not need a static IP address. But if you want to host your own server, you must have a static IP address. It ensures your email address and sites tied to a static IP address have the same IP consistently. As a result, external devices can find you easily on the internet.

Dynamic IP address: These IP addresses change regularly and automatically, unlike static addresses. ISPs have a pool of unassigned IP addresses, which they assign to customers who sign in to their internet service. A customer uses the assigned IP address as long as they are connected to the internet. When the customer stops using the service or disconnects from the internet, the assigned IP address becomes free and returns to the pool of unassigned IP addresses. These dynamic addresses are re-assigned to other customers.
This approach saves ISPs costs, and they don’t need to perform specific tasks to re-establish a user’s IP address time and again. In addition, it also ensures security as changing IP addresses makes it difficult for hackers to zero in on one user.

We have earlier discussed static IP addresses for businesses wanting to own a server for their sites. Similarly, there are website IP addresses of two types as well.

#3. Shared and Dedicated IP address
Shared IP address: Website owners relying on a shared hosting service from a web host will get a server shared by other sites. It is suitable for small-scale businesses, bloggers, portfolio sites, etc., where traffic is less. They will have a shared IP address.
Dedicated IP addresses: Larger sites are looking for a more secure option, and pro gamers who want better control over their servers can go for dedicated hosting plans. They can buy a dedicated IP address. It helps you obtain SSL certificates easily and lets you run your FTP server.
Hence, you can share files with different people securely within your organization or go anonymous. Furthermore, you can even access your site with your IP address instead of your domain name.

4. Logical and Physical
Logical IP address: It is assigned by the software inside a server or router and may or may not change periodically. For instance, your laptop can have a different IP address if you connect it to another hotspot.
Physical IP address: Every hardware unit is built with a unique IP address that never changes. This is a physical IP address. You can use a resolution protocol to convert a logical IP address to a physical one to identify a device in your IP network.
=======================
Public IP Addresses
A public IP address is an address where one primary address is associated with your whole network. In this type of IP address, each of the connected devices has the same IP address.

This type of public IP address is provided to your router by your ISP.

Private IP Addresses
A private IP address is a unique IP number assigned to every device that connects to your home internet network, which includes devices like computers, tablets, smartphones, which is used in your household.

It also likely includes all types of Bluetooth devices you use, like printers or printers, smart devices like TV, etc. With a rising industry of internet of things (IoT) products, the number of private IP addresses you are likely to have in your own home is growing.

Dynamic IP address
Dynamic IP addresses always keep changing. It is temporary and are allocated to a device every time it connects to the web. Dynamic IPs can trace their origin to a collection of IP addresses that are shared across many computers.Dynamic IP addresses are another important type of internet protocol addresses. It is active for a specific amount of time; after that, it will expire.

Static IP Addresses
A static IP address is an IP address that cannot be changed. In contrast, a dynamic IP address will be assigned by a Dynamic Host Configuration Protocol (DHCP) server, which is subject to change. Static IP address never changes, but it can be altered as part of routine network administration.

Static IP addresses are consistent, which is assigned once, that stays the same over the years. This type of IP also helps you procure a lot of information about a device.

Types of Website IP Addresses
Two types of website IP Addresses are 1) Share IP Address 2) Dedicated IP Address

Shared IP Addresses
Shared IP address is used by small business websites that do not yet get many visitors or have many files or pages on their site. The IP address is not unique and it is shared with other websites.

Dedicated IP Addresses:
Dedicated IP address is assigned uniquely to each website. Dedicated IP addresses helps you avoid any potential backlists because of bad behavior from others on your server. The dedicated IP address also gives you the option of pulling up your website using the IP address alone, instead of your domain name. It also helps you to access your website when you are waiting on a domain transfer.

Subnetting and Sub Masks:
While subnet masks are an essential part of subnets, they are not the same thing.
Subnetting is a practice of dividing a network into smaller networks.

Subnet Marks - is a 32 bits address used to distinguish between a network address and a host address in IP address, however a sub mark identifies which part of an IP address is the network address and the host address, these are idenitfied inside the data packets travelling over the internet.

Why use subnetting? Subnetting serves a number of purposes. From giving administrators more control over their networks and improving their networks’ performance. To boosting security and making more efficient use of IP addresses. Here are some of the key benefits.
=More efficient routing of data: By dividing broadcast domains, subnetting reduces the number of nodes that broadcast traffic interacts with and makes the routing of data packets more direct and efficient.
Subnet masks are key here. That’s because a subnet mask is what makes sure that traffic stays contained within its designated subnet. This reduces major congestion and the load imparted on the network. 

Subnetting effectively decreases the distance that data packets need to travel in the network. This also allows the network to route data more efficiently. 

All of this increases the speed and overall performance of the network. 
= Better network security: If you’re operating a large local network, with many connected devices and a high volume of network traffic, there are a number of security advantages of running multiple subnets rather than one larger network. 

Most notably, if a subnet is compromised by an attack, only that network segment will be affected. Using subnets, instead of all devices on the same network being visible to attackers, they would only have access to other devices on the same subnet. 
You may want to create subnets to keep legitimate local network traffic siloed, too. Subnets make it possible to prevent all devices from accessing the entire network. This is a great solution if you want to keep certain files or processes secure or limit remote network access.
=Increased lifespan of IPv4: When the internet was first coming into use, it was easy to get an IP address. Since there is a limited number of possible IPv4 addresses, the available IP address stock quickly began to diminish. 

Looking for an IP address solution, creative minds came up with the idea of using subnetting to increase the utility of a single public IP address. 

Instead of each device having a unique IP address, a network can have a number of private IP addresses on a single IP network. This means that each device on an IP network has an IP address with a part that refers to the overall network IP address, and a part that refers to its subnet. 

This is why IPv4 remained the internet standard for much longer than if subnetting was not an option. 

CIDR Notation and Address Aggregation
What is CIDR - Classless Inter-Domain Routing (CIDR) is a method of IP address allocation and IP routing that allows for more efficient use of IP addresses. CIDR is based on the idea that IP addresses can be allocated and routed based on their network prefix rather than their class, which was the traditional way of IP address allocation.

CIDR addresses are represented using a slash notation, which specifies the number of bits in the network prefix.

IP Address Aggregator - is a utility developed to automate minimization process and convert bunch of IPv4 addresses into smallest continuous range(s) possible. IP aggregation is commonly performed by network engineers working with BGP & routers. This utility will help webmasters to configure server firewalls, apache .htaccess files, address masks and so on.

Basic Usage

IP Address Aggregation Tool accepts various IP address formats for input (scroll to Input Format Examples for more details). Enter IP Address list in a block of text (one IP Address or range per line) into IP Address Ranges input area. Select desired output format and click submit button. It will automatically discard any non-recognized or invalid address text. To use the IP aggregator click this link: https://tehnoblog.org/ip-tools/ 

IP Address Classes and Provate IP Address Ranges
https://www.guru99.com/ip-address-classes.html
How does IP address work?
IP address works in an IP network like a postal address. For example, a postal address combines two addresses, address, or your area your house address.
The address or your area is a group address of all houses that belong to a specific area. The house address is the unique address of your homes in that area. Here, your area is represented by a PIN code number.
In this example, the network address comprises all hosts which belong to a specific network. The host address is the unique address of a particular host in that network.

What is Classful Addressing?
Classful addressing is a network addressing the Internet’s architecture from 1981 till Classless Inter-Domain Routing was introduced in 1993.

This addressing method divides the IP address into five separate classes based on four address bits.

Here, classes A, B, C offers addresses for networks of three distinct network sizes. Class D is only used for multicast, and class E reserved exclusively for experimental purposes.

Let’s see each of the network classes in detail:


Class A Network
This IP address class is used when there are a large number of hosts. In a Class A type of network, the first 8 bits (also called the first octet) identify the network, and the remaining have 24 bits for the host into that network.

An example of a Class A address is 102.168.212.226. Here, “102” helps you identify the network and 168.212.226 identify the host.

Class A addresses 127.0.0.0 to 127.255.255.255 cannot be used and is reserved for loopback and diagnostic functions.

Class B Network
In a B class IP address, the binary addresses start with 10. In this IP address, the class decimal number that can be between 128 to 191. The number 127 is reserved for loopback, which is used for internal testing on the local machine. The first 16 bits (known as two octets) help you identify the network. The other remaining 16 bits indicate the host within the network.

An example of Class B IP address is 168.212.226.204, where *168 212* identifies the network and *226.204* helps you identify the Hut network host.

Class C Network
Class C is a type of IP address that is used for the small network. In this class, three octets are used to indent the network. This IP ranges between 192 to 223.

In this type of network addressing method, the first two bits are set to be 1, and the third bit is set to 0, which makes the first 24 bits of the address them and the remaining bit as the host address. Mostly local area network used Class C IP address to connect with the network.

Example for a Class C IP address:

192.168.178.1

Class D Network
Class D addresses are only used for multicasting applications. Class D is never used for regular networking operations. This class addresses the first three bits set to “1” and their fourth bit set to use for “0”. Class D addresses are 32-bit network addresses. All the values within the range are used to identify multicast groups uniquely.

Therefore, there is no requirement to extract the host address from the IP address, so Class D does not have any subnet mask.
Example for a Class D IP address:

227.21.6.173

Class E Network
Class E IP address is defined by including the starting four network address bits as 1, which allows you two to incorporate addresses from 240.0.0.0 to 255.255.255.255. However, E class is reserved, and its usage is never defined. Therefore, many network implementations discard these addresses as undefined or illegal.

Example for a Class E IP address:

243.164.89.28

Limitations of classful IP addressing
Here are the drawbacks/ cons of the classful IP addressing method:

Risk of running out of address space soon
Class boundaries did not encourage efficient allocation of address space

----------------------
Advanced Topices in IP Addressing- this involves the study of advanced technologies and techniques for managing and optimizing  performance, these may include:
Routing protocols: routing protocol specifies how routers communicate with each other to distribute information that enables them to select paths between nodes on a computer network, can also be  rules that routers use to communicate and find the best paths for data packets across networks.
Virtual Private Networks(VPNs): A virtual private network, or VPN, is an encrypted connection over the Internet from a device to a network. The encrypted connection helps ensure that sensitive data is safely transmitted. It prevents unauthorized people from eavesdropping on the traffic and allows the user to conduct work remotely. 
Quality of Service(QoS): Set of technologies and techniques that are used to manage and optimize network performance
Domain Name System (DNS): The Domain Name System (DNS) is the Internet's system for mapping alphabetic names to numeric Internet Protocol (IP) addresses like a phone book maps a person's name to a phone number.
Network Address Translation (NAT): It’s a way to map multiple private addresses inside a local network to a public IP address before transferring the information onto the internet. 