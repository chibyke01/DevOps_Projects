# AWS NETWORKING IMPLEMENTATION (VPC, SUBNETS, IG, NAT, ROUTING)

In this project we learn how the implementation of VPC, subnets, internet gateways, NAT and routing can be used to deploy scalable and secure cloud architectures.

In my previous project I have explained in details(VPC, SUBNETS, SUBMASKS, IG, NAT and ROUTING) and in this project we see how the application of these configurations can assist to protect our cloud resources and architectures.

## VPS Creation and Subnet Configuration
* **What is an Amazon VPC**

An **Amazon Virtual Private Cloud(VPC)** is a private section of Amazon cloud, where one can manage resources (like servers or databases)
 
The main steps to creating a VPC and configuring core networks services are covered in the following steps as listed below:
1. Default VPC
2. Creating a new VPC
3. Creating and configuration of subsets

**The Default VPC** - It is just like a starter pack that is preconfigured within the Amazon cloud where you can start deploying applications or services, it is a built-in security and network settings to help get started but can be adjusted to fit your personal configuration.

**Creating a new VPC** - This is process involves setting up your choice configuration for the VPC. In the course of this project we will be using the **VPC only** option as VPC and more option will be later.
Enter the name tag as **"first-vpc"** and **"10.0.0.0/16"** as the **IPv4 CIDR**. The "10.0.0.0/16" will be the **primary IPv4 block** and **"100.64.0.0/16"** can be added as the **secondary IPv4** block e.g., the secondary CIDR block can be used when running out of IPs and the need to add additional blocks or when there is a VPC with overlapping CIDR which will need to be connected or peer.
   
See the below screenshots on how to create a VPC

As soon as the VPC is created a **vpc-id** is assigned and a **route table** is created automatically that serves as the main route table **(rtb)**
At this we have VPC and route table created but wont be able to put anything inside however if we try to create an EC2 instance we cant proceed as it requires subnets. 

Creating and Configuring Subnets
---------------------------------
**What is Subnets?** - Subnets are like smaller segements within a VPC that helps organize and manager resources, they are created to organize and manager network effectively.

Follow the below steps to create the Subnet
Go to VPC
Subnets
Create subnets and select the VPC that was created
However if you do not choose a zone it will automatically or rondomly pick a zone for you buy AWS.

```
subnet-public1a eu-north-1a 10.0.11.0/24
subnet-public2b eu-north-1b 10.0.12.0/24
subnet-private1a eu-north-1a 10.0.1.0/24
subnet-private2b eu-north-1b 10.0.2.0/24
```

After creating these subnets we can deploy our EC2 instances into the created VPC by selection one of the subnets, but the public subnet does not have any internet access at this stage. 

Unstanding Public and Private Subnets in AWS VPC.
------------------------------------------------
In the world of AWS VPC, subnets can be likened to be a plots on a land(VPC) and these plot(subnets) have a direct road access (internet access) - these can be said to be Public subsets. others are more private or with no direct road access which can be likened to be Private Subnets.

Creating a Public Subnets
-------------------------
Go to the AWS VPC page 
Find Subnets click on it, then Create subnet
Give it a name 
Attach an internet Gatway to the subnet to provide internet access
Update the route table associated with the subnet to allow to flow to and from the internet.

Creating a Private Subnet
-------------------------
Go to the AWS VPC page 
Find Subnets click on it, then click subnet, give it a name  and leave the IP settings as they are.
Do not attach an internet Gatway to the subnet to provide internet access
Update the route table associated with the subnet to allow to flow to and from the internet.

Public subnets are great for resources that needs to connect to the internet =, like webservers while Private subnets are great for resources that you dont want to be exposed to the internet like databases.

Internet Gaetway and Routing Table
---------------------------------
What is Internet Gateway
Internet Gateway is a VPC component that allows communication between your VPC and the internet. It supports IPv4 and IPv6 traffic. It does not cause availability risks or bandwidth constraints on your network traffic.

Technically the created subnets are still private this will be made public by attaching an internet Gateway to it and this follows the below systematical order as listed below:
* An internet Gateway (IGW) attached to VPC
* Route table with default route towards the IGW
* Public IP assigned to the AWS resources (e.g., EC2 instances)

To create the IGW follow the steps as shown in the screenshot.
Go to VPC, Internet Gateways and click Create internet gateway.

What is Routing Table? - routing table, or routing information base (RIB), is a data table stored in a router or a network host that lists the routes to particular network destinations, and in some cases, metrics (distances) associated with those routes. The routing table contains information about the topology of the network immediately around it. In the context of this project we can say its a map guilding your resources on how to get to in and our of the VPC.

Creating and Configuring Routing Tables

Once its created, edit the route table add a default route to the Internet Gateway(IGW) as shown below:

Next go to "Subnet associations" tab and click "Edit subnet associations"

Note: 
test-vpc-public-rtb: A route table with a target to Internet gateway is a publice route table
test-vpc-private-rtb: A route table with a target to NAT gateway is a private route table


NAT Gateway and Private Subnets
Introduction to Private Subnets and NAT Gateway

In AWS Virtual Private Cloud(VPC), private subnets are secluded areas where you can place resources that should not be directly exposed to the internet, but if the resources wants to access the internet for updates or downloads that is when the NAT Gateway comes in.

Network Address Translation(NAT) allows instances in the private subnet to connect to the outside services but restricts external services to connecting to these instances.

Creating a NAT Gateway and Linking it to a Private Subnet
Go to VPC
NAT Gateway 
Click Create NAT Gateway 
Give it a name
On the Subnet Tab choose the created private subnet
Allocate an Elastic IP as this required for the creation of NAT gateway.

Create a Route table by editing the route table to add a default route to the NAT Gateway.

Go to Subnet associations tab and click Edit subnet associations and check the two private subnets.

From the above setup we have seen how these configurations can be used to maintain security while allowing necessary internet access for the resources.


Security Group and Network ACLs
Understanding the Difference between Security Groups and Newtwork Access Control List (NACLs)
Security Group (Add diagram) These are for controlling user access to resources, a security group examines the IP addresses and ports of incoming and outgoing network traffic, it acts as a virtual firewall that filters traffice based on predefined rules. These rules specifies which type of traffic are allowed or denied.

Security group can be configured to allow incoming HTTP traffic on port 80 ro a web server but blocks all other types of incoming traffic. similarly it can permit outgoing traffic from the web server to external databases on a specific port while restricting all other outbound connections. 

Overall, security groups provide an essential layer of security for cloud resources by allowing us to define and manage access control policies.

Network Access Control List(NACLs) (Diagram) -  is a security layer for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets.

It ic configured to allow incoming SSH(secure shell) traffic on port 22 to a specific subnet while blocking all other types of incoming traffic. it can also permit outgoing traffiv from the subnet to a specific range of IP addresses on certain port while disallowing any other outbound connections

However its important to note that Network ACLs operate at the subnet level, they control traffic for all instances within a subnet, they provide a broder scope of security compared to security groups which operate in instance level.

Network ACLs function as a virtual security guard for subnets by regulating inbound and outbound traffice at broader level.

VPC Peering and VPN Connection
-----------------------------