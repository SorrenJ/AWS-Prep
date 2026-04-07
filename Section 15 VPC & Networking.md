
# IP Addresses

IPv4 - Internet Protocol version 4 (4.4 billion addresses) 

charged $0.005 per hour 

## Public IPv4
Reachable from the internet when associated with an internet gateway


## Private IPv4 
Used for communication within a VPC and btwn peered VPCs or VPN-connected networks
Can be used on private networks (LAN) such as internal AWS networking
it is fixed for EC2 instances even if you start/stop them

## Elastic IP

allows you to attach a fixed public IPv4 address to EC2 instance

###  Elastic IP vs. Regular Public IP

|Feature|**Elastic IP (EIP)**|**Regular Public IP (Default)**|
|---|---|---|
|**Static vs. Dynamic**|**Static**: The address never changes unless you explicitly release it[](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/elastic-ip-addresses-eip.html).|**Dynamic**: The address can change when you stop and restart the instance[](https://notes.kodekloud.com/docs/AWS-Solutions-Architect-Associate-Certification/Services-Networking/Elastic-IP/page).|
|**Ownership**|**Account-Owned**: The IP is allocated to your AWS account and remains yours until you release it[](https://notes.kodekloud.com/docs/AWS-Solutions-Architect-Associate-Certification/Services-Networking/Elastic-IP/page).|**AWS-Owned**: The IP is assigned from AWS's public pool. When the instance stops, the IP is released back into the pool.|
|**Re-assignability**|**Yes**: You can easily remap an EIP from one instance to another, enabling quick failover[](https://docs.aws.amazon.com/ja_kr/vpc/latest/userguide/vpc-eips.html).|**No**: You cannot move a standard public IP to another instance.|

### 💡 Key Benefits of Using an Elastic IP

The ability to own and remap a static IP provides several practical benefits:

- **High Availability & Fault Tolerance**: If an EC2 instance fails or needs maintenance, you can quickly reassign its EIP to a healthy, replacement instance. This masks the failure from users and keeps your application accessible[](https://docs.aws.amazon.com/ja_kr/vpc/latest/userguide/vpc-eips.html).
    
- **Consistent Endpoint**: An EIP provides a permanent public IP address, which is crucial for a stable connection. For example, when hosting a website, you can point your domain's DNS record to the EIP and be confident it won't break if the underlying server restarts[](https://tsecurity.de/de/2416510/IT+Programmierung/Mastering+AWS+Elastic+IPs%3A+A+Beginner%27s+Guide+to+Consistent+Cloud+Connectivity/de/2313993/Inhalte%20hinzuf%C3%BCgen/).
    
- **Simplified Configuration**: You can whitelist an EIP in firewall rules or use it as a stable endpoint for external services, avoiding frequent updates to configurations tied to a changing IP address[](https://docs.aws.amazon.com/ja_kr/vpc/latest/userguide/vpc-eips.html).
    
- **Enhanced Control**: You have full control to allocate, associate, and disassociate EIPs as your infrastructure evolves, providing flexibility for blue/green deployments or testing scenarios[](https://docs.aws.amazon.com/ja_kr/vpc/latest/userguide/vpc-eips.html).

## IPv6
Internet Protocol version 6 

every IP address is public in AWS (no private range)

free


# AWS OSI Layers

**Layer 7**

AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to an Amazon API Gateway API, Amazon CloudFront or an Application Load Balancer. HTTP and HTTPS requests are part of the Application layer, which is layer 7.

**Layer 3** - Layer 3 is the Network layer and this layer decides which physical path data will take when it moves on the network. AWS Shield offers protection at this layer. 

**Layer 4** - Layer 4 is the Transport layer and this layer data transmission occurs using TCP or UDP protocols. AWS Shield offers protection at this layer. 

# VPC


Virtual Private Cloud  a private network to deploy your resources

 It's like setting up a private data center in the cloud where you have complete control over your virtual networking environment


You can define your own IP address range, create subnets, and configure route tables and network gateways

 spans all of the Availability Zones (AZ) in the Region

Every AWS account comes with a ready-to-use default VPC in each region

Custom VPC: for production workloads or when you need specific network configurations

can contain subnets

CIDR range -> shows a range of IP addresses  that is allowed within your VPC
## Subnet

spans only one Availability Zone (AZ) in the Region

A subnet is a range of IP addresses within your VPC

You can think of it as a way to divide your VPC's network into smaller, more manageable sections

Allows you to partition your networks inside your VPC


![[Screenshot 2026-02-19 222255.png]]


### Public subnet 


is a subnet that is accessible from the internet

Has a direct route to an internet gateway. Resources in a public subnet can directly access the public internet.

For example you can place load balancer

spans only one Availability Zone (AZ) in the Region
### Private subnet

private subnet is a subnet that is not accessible from the internet

Does not have a direct route to an internet gateway. For resources in a private subnet to access the internet (e.g., to download updates), they must use a NAT device.

For example You can place your databases since they dont need access to the internet -> more secure

You can define a private subnet through a route table



![[Screenshot 2026-02-20 000109.png]]

So if we look at a VPC, a more complete one, we have the Cloud of AWS, we'll have Regions,

within a Region, we'll have a VPC, and the VPC will have what's called a CIDR Range, which is a range of IP addresses that is allowed within your VPC.
And then the VPC can go across two or three availabilities zone, so we have AZ 1 that contains a public subnet and a private subnet, and AZ 2, which contains also a public subnet and a private subnet.

So in this example, we have two AZ, one VPC, four subnets, two of them are public, and two of them are private, and we can launch EC2 instances in each of these subnets.

# VPC Gateways
### Internet Gateways

Helps our VPC instances connect with the internet 

as soon as we have a internet gateway and a route to the internet gateway, that makes the subnet a public subnet

### NAT Gateways

Now, if you have an instance in a private subnet, it is not going to be accessible from the internet,

but you may want to give it access to the internet, for example, to get updates for your operating system or to download files.

So for this, we can create what's called a NAT Gateway,

will allow your instances in your private subnet to access the internet while remaining private


# VPC Lines of defense 
## Network ACL (NACL)

A network access control list (network ACL) is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets (i.e. it works at subnet level). A network access control list (network ACL) contains a numbered list of rules. A network access control list (network ACL) evaluates the rules in order, starting with the lowest numbered rule, to determine whether traffic is allowed in or out of any subnet associated with the network ACL.

 a firewall that is controlling traffic from and to the subnet. So remember it is at the subnet level

So remember it is at the subnet level in which we can define, ALLOW or DENY rules and then attach at the subnet level and the rules can only include IP addresses.

Key points:
- Operates at the subnet level
- Supports ALLOW rules and DENY rules
- is stateless: Return traffic MUST be explicitly allowed by rules






![[network-acl-basics.jpg]]



## Security Groups

A firewall that controls traffic to and from an EC2 Instance 

Can only ALLOW rules they can reference either IP addresses and other security groups.

Key points:
- Operates at the instance level
- Supports ONLY ALLOW rules 
- is stateful: Return traffic is AUTOMATICALLY allowed, regardless of any rules


![[security-group-basics 1.jpg]]
## Comparisons

![[Screenshot 2026-02-20 123124.png]]




So in this example, we have the security group around our EC2 instance, and that controls the traffic going in and out of our EC2 instance. 

So the security group and the NACL are quite different. The NACL is at the subnet level and the security group is at the EC2 instance level.


![[Pasted image 20260220123313.png]]




# VPC Flow Logs

VPC flow logs are a log of all the IP traffic going through your interfaces.

captures information about IP traffic going into your interface

Similar to subnet flow logs and elastic network interface flow logs

By enabling the flow log, we can monitor and troubleshoot for connectivity issues, for example, if a subnet can not connect to the internet or a subnet cannot connect to another subnet or the internet cannot access a subnet, this would be captured by the VPC flow log and we can look at it to get to the root cause of it.

we also get information for Elastic Load Balancers, ElastiCache, RDS, Aurora, et cetera, And VPC flow logs can go to Amazon S3, CloudWatch Logs and Amazon Data Firehose.






# VPC Peering

Connect 2 VPCs privately using AWS network and make them behave as if they were part of the same network 

![[Screenshot 2026-02-20 101208.png]]


So this is an example, We have VPC A and VPC B and we can peer them together and as soon as it's done, then they will have the same network or behave as if they were in the same network.


So for this, you need to make sure that the IP addresses range do not overlap. If they do overlap, then you cannot establish a VPC peering connection.

 VPC peering connection

is not transitive. -> That means that if you add a new VPC, for example VPC C, and you create a peering connection between VPC A and VPC C, then that means that VPC B and C cannot talk to each other yet.

If you want to have VPC B and C talk to one another, then you will need to create another peering connection between your VPC B and C.


# VPC Endpoints

Endpoints allow you to connect to AWS Services using a PRIVATE network instead of a public https

Gives you enhanced security and lower latency to access AWS services

Types:

VPC gateway endpoint -> is for Amazon S3 and DynamoDB only

VPC endpoint interface -> to connect to any other services on AWS, for example, CloudWatch,



![[Screenshot 2026-02-20 130116.png]]
Example:

We have a VPC, a private subnet and an EC2 instance in that private subnet and we want to connect to Amazon S3 or DynamoDB.

For this, we create a VPC endpoint of type gateway, so you have to remember this, the gateway endpoint is for Amazon S3 and DynamoDB only,

and using this EC2 instance, you can connect through the gateway into Amazon S3 and DynamoDB, but privately.

The other type of endpoint you have is a VPC endpoint interface, which is to connect to any other services on AWS, for example, CloudWatch, if you wanted to push a custom metric from your EC2 instance into the CloudWatch service.


# PrivateLink (VPC Endpoint Services)

Private Link allows you to connect a service running within your VPC to other VPCs directly and privately. 

So it does not require VPC peering or internet gateway, because it's from the private network, or NAT or route tables or anything like this.

Requires 
- Network Load Balancer to expose that service to you
- Elastic Network Interface for yourself
- Establishing a private link -> so that you have private access to their Network Load Balancer and therefore to their service

![[Screenshot 2026-02-20 131341.png]]




for example, 

you are talking to a vendor on the AWS Marketplace, and they run application service. So they have their own service that you wanna use in their own VPC. And you wanna have access to it from your own VPC in your own accounts with your own consumer applications.

In that case, you're going to ask your vendor to do a Private Link.

On their end, they will have to create a Network Load Balancer to expose that service.

And on your end, you will create an Elastic Network Interface, and then you will establish a Private Link between the two so that you have private access to their Network Load Balancer and therefore to their service.

And all the internet traffic is actually not gonna go through the public internet, but it's actually gonna go through your private network.

And so therefore all communications will remain private. And so for every new customer that third party will need,

all they will have to do is to create a new Private Link for their customers, which is very easy to manage and way more scalable.


# Site to Site VPN & Direct Connect


So say you have an on-premises data center. This is your own data center, and you want to connect it to the cloud, to your VPC.


![[Screenshot 2026-02-20 190814.png]]



For this, you have two options.
## Site-to-site  Virtual Private Network VPN

This is to connect your on-premises VPN to AWS

VPN: it is a connection between your on-premises data center and VPC that is going to be encrypted, and that goes over the public internet

Pros
- No one else can access to communication 
	- Your on-premises data center will connect to your VPC through the public internet, and then it will be encrypted. 

- Set up very quickly 
	- In about five minutes, you can have a connection between your data center in AWS.

Cons
- May have some limited bandwidth

- you may have some security concerns, even though it is obviously encrypted.

Requirements
- CGW 
	- we need on-premises a customer gateway or CGW,

- VGW
	- you will need virtual private gateway, or VGW and 

once the two things are provisioned and created, then you can connect them together using a site-to-site VPN.

![[Screenshot 2026-02-20 190708.png]]



## Direct Connect DX

Establish a private physical connection between on-premises and AWS

Pro
- Direct connect, is to establish a natural physical connection between your on-premises data center and AWS.
- Private Connection 
	- private, secure and fast. And it will go over the private network.

Con
a lot more expensive
- because you have to do a physical connection between yourself and a direct connect partner into AWS.
-  will take at least a month to establish this. But it's going to be more private and obviously faster and more reliable.

# ClientVPN

you have your computer and you want to privately connect into your AWS VPC. Therefore you will leverage the client VPN to establish a connection using the open VPN to your private network in AWS or on premises

Well, for example say you have deployed EC2 instances in a private VPC and you want to access them using a private IP. Well, that's difficult if you don't have a VPN but if you have a VPN, then it's super easy.

Once the VPN connection is established you will be able to access your EC2 instances using their private IP just as if you were in the VPC network yourself.

So your VPC is right here and then your client's VPN is installed on your computer. You will establish the VPN connection over the internet.

So this goes over the public internet, of course. And then you will be as if you are connected privately into your VPC.

And if your VPC has established a site to site VPN connection to your on-premises data center then your computer will also be able to access, privately, your servers on your, on premises data center.

Key points:

- Connect from your computer using OpenVPN
- Allows you to connect to your EC2 instances over a private IP (just as if you were in the private VPC network)
- Goes over public internet
![[Screenshot 2026-02-21 130725.png]]


# Transit Gateway

a way to connect hundreds or thousands of VPC together, with as well your on-premise infrastructure

has a peering connection between thousands of VPC and your on-premises system with a hub-and-spoke star connection

You have the VPC Transit Gateway in the middle, and all your Amazon VPC, your Direct Connect gateway, as well as your VPN connections are connected through the Transit Gateway

Pro

you don't need to peer the VPC with one another, you don't need to have different connections and routes between each of them and Direct Connect and side to side VPN, all of this is done within a single gateway

![[Screenshot 2026-02-21 133324.png]]


# Quiz

Question 1:

Your private subnets need to connect to the Internet while still remaining private. Which AWS-managed VPC component allows you to do this?

NAT Gateways

allow your instances in your private subnets to access the Internet while remaining private, and are managed by AWS

Question 2:
A public subnet is accessible from the Internet while a private subnet is not accessible from the Internet.

Yes

a public subnet is accessible from the internet while a private subnet is not accessible from the internet

Question 3:
Which type of firewall has both ALLOW and DENY rules and operates at the subnet level?

Network Access Control List (NACL)

A network access control list (NACL) is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets. They have both ALLOW and DENY rules

Question 4:
You would like to connect hundreds of VPCs and your on-premises data centers together. Which AWS service allows you to do link all these together efficiently?

Transit Gateway

connects thousands of VPC and on-premises networks together in a single gateway


Question 5:

A company needs two VPCs to communicate with each other. What can they use?

VPC Peering


Question 6:
You need a logically isolated section of AWS, where you can launch AWS resources in a private network that you define. What should you use?


A VPC 

A virtual network dedicated to your AWS account, It is logically isolated from other virtual networks in the AWS cloud. You can launch your AWS resources, suc as Amazon EC2 instances, into your VPC


Question 7:

A company needs to have a private, secure, and fast connection between its on-premises data centers and the AWS Cloud. Which connection should they use?

AWS direct connect 

AWS Direct Connect is a cloud service solution that makes it easy to establish a dedicated private network connection from your premises to AWS

Question 8:

Your VPC needs to connect with the Internet. Which VPC component can help?

Internet Gateway

an internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between your VPC and the internet