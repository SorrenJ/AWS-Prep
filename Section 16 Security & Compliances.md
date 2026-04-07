# AWS Shared Responsibility Model

## RDS

AWS responsibility:
• Manage the underlying EC2 instance, disable SSH access
• Automated DB patching
• Automated OS patching
• Audit the underlying instance and disks & guarantee it functions

 Your responsibility:
• Check the ports / IP / security group inbound rules in DB’s SG
• In-database user creation and permissions
• Creating a database with or without public access
• Ensure parameter groups or DB is configured to only allow SSL connections
• Database encryption setting


## S3

AWS responsibility:
• Guarantee you get unlimited storage
• Guarantee you get encryption
• Ensure separation of the data between different customers
• Ensure AWS employees can’t access your data
Your responsibility:
• Bucket configuration
• Bucket policy / public setting
• IAM user and roles
• Enabling encryption

# DDOS Protection

A DDoS attack is a Distributed Denial-of-Service attack



In this case they're going to launch multiple master servers and these servers are going to launch bots,

all these bots are going to send a request to our application server.

Now our server is not meant to handle this many requests so it will be overwhelmed and it will not be working anymore, he will be denied a service and therefore any normal user trying to connect to our application server, will see that our server is not accessible or not responsive,


 AWS you can protect yourself from it.
## AWS Shield Standard

it will protect you against a DDoS attack or your websites and application.

Free service for every AWS customer

Provides protection from attacks such as SYN/UDP Floods, Reflection attacks
and other layer 3/layer 4 attacks

## AWS Shield Advanced:
If you want a premium DDoS protection, you have to use AWS Shield Advanced which is going to give you 24/7 so 24 hours a day, seven days a week protection on DDoS.

Protect against higher fees during usage spikes due to DDoS
## WAF Web Application Firewall

 filter specific requests based on rules, this is the web application firewall.

Define Web ACL (Web access control list)
Filtering Ip address, HTTP headers, HTTP body, URI Strings

protects against SQL injections and cross-site scripting (XSS)

size constraints - make sure requests are not too big

geomatch (block certain countries)

rate-based rules to count the occurences of events like user cannot do more than 5 requests per second

Protects your web applications from common web exploits (Layer 7) 

Layer 7 is HTTP (vs Layer 4 is TCP)

Can be deployed only on HTTP friendly devices, so it can be deployed on your application load balancer





## CloudFront and Route 53

• Availability protection using global edge network
• Combined with AWS Shield, provides attack mitigation at the edge

## Architecture

![[Screenshot 2026-03-04 205035.png]]

So we have our users and they will be routed through the DNS on Route 53 which is protected by shield

so your DNS is safe from DDoS attack, then you should use a CloudFront distribution to make sure your content is cached at the edge and then it is also protected by shield

In case you need to filter and protect from an attack, you can use the web application firewall. To serve that application you can use a load balancer in the public subnet that will scale for you and finally behind the load balancer you should use EC2 instances

in an auto scaling group to be able to scale to the higher demand. So all of this will give you a really good DDoS protection against these type of attacks.


# Network Firewall

Protects your entire VPC all at once from layer 3 to layer 7 protection in any direction:
- VPC to VPC traffic
- Outbound to internet
- Inbound from internet
- to and from your direct connect and site to site VPN.

This is a much better protection from network firewall, than using, for example, network SCLs -> operates at the subject level


# Firewall Manager

Manages security rules in all accounts of an AWS Organization



- VPC security groups for EC2, load balancer

- WAF rules

- AWS Shield Advanced

- AWS Network Firewall


applied to all the current and future accounts and for all the resources as they are being created in these accounts, really allowing you to have the certainty that the rules are managed across all accounts at any point of time.

# Penetration Testing

Users can preform security assessments or penetration tests against their AWS infrastructure 

It doesnt need prior apporval and don't need an authorization for 8 various services like EC2, RDS, CloudFront, Auora, API Gateways, Lambda, Lightsail, Elastic Beanstalk

Prohibited activities: DNS zone walking, simulated DDoS, Port flooding, Protocol Flooding, Request flooding


# Data at rest

Data is stored or archive on a physical device 

Examples: hard drive or hard disk, rds instance, S3 buckets, encrypted data at rest on an EFS network drive, encrypted data on S3

Not moving but written somewhere


# Data in transit

data being moved from one location to another

Examples: when you move from between an EC2 instance and a DymamoDB table, EFS to S3




# Key Management Service KMS

we can encrypt the data. That means that someone who does not have access to these encryption keys, even if they had access to our data, they could not decrypt it, and they could not read it, and therefore it's protected.

KMS is the encryption service at the center of AWS

In KMS, we don't have access to the keys. AWS WILL MANAGE the keys for us, we just define who can access these keys

Encryption Opt-in

Example: 

for your EBS volumes, you can choose to encrypt them with KMS

For S3 buckets, you also have the option to do server-side encryption of objects.


## Types of KMS Keys

### Customer Managed Key

Create, managed and used by the customer

enable or disable a specific key, 

define rotaion policy (wanting a new key to be generated every year)

bring your own key?

### AWS Managed Key

created, managed and used on the customer's behalf by AWS

whenever an AWS service has some encryption managed by AWS,  whenever a key name is aws/s3 or aws/ebs

### AWS Owned Key

a collection of keys that a service owns and manages to use in multiple accounts

So AWS can use these keys to protect some resources in your accounts, but you actually don't have any power to view the keys.


# CloudHSM

AWS will just provision to us the encryption hardware, but managing the keys ourselves

HSM module is a dedicated hardware for security, WE MANAGE OUR OWN encryption keys entirely, not AWS



![[Screenshot 2026-03-05 192904.png]]



AWS will manage the hardware. So they will manage the device I just showed you,
but we use the CloudHSM service with the CloudHSM clients to manage the keys. And obviously, the connection between our clients and CloudHSM is encrypted so that we can manage the keys securely


### CloudHSM Keys (Custom keystore)

keys are generated from your own CloudHSM hardware device

 all the cryptographic operations will be performed within the CloudHSM cluster.


# AWS Certificate Manager

a service to to easily provision, manage and deploy SSL/TLS certificates

certitificates are used to provide in-flight encryptions for your websites by providing an HTTPS endpoints

ACM supports both public and private TLS certificates

 it is free of charge for public TLS certificates.

And it has integration, that means that it loads the TLS certificates on different services. It could be your elastic load balancer, your CloudFront distributions or your API is on API gateway



![[Screenshot 2026-03-05 230649.png|290]]


We have our application load balancer and it is connected in the backend through HTTP to an auto scaling group with our EC2 instances. But we want our end users to have HTTPS exposed on our application of answer.

So to do so we're going to use ACM.  And ACM once it's connected to our domain is going to be allowing us to provision and maintain these TLS certificates. They will be loaded onto our application load balancer and then automatically the load balancer will be able to offer HTTPS as an end point for our clients, which allows us to get in-flight encryption over the public web.