
# Global applications

Deployed in multiple geographies, could be regions and or edge locations

**Decreased Latency** -> latency is the time is takes for network packet to reach server

**Disaster Recovery (DR)** -> if an AWS region goes down, u can fail-over to another region so the app can still work, important to increase availability

**Attack Protection** -> distributed global infrastructure is harder to attack

Regions: for deploying apps and infrstucture

Availability zones (AZ) : Made of multiple data centers

Edge Locations: For content delivery as close as possible to users

# Route 53

This is a Managed Domain Name System (DNS)

A collection of rules and records -> helps clients understand how to reach a server url

www.google.com => 12.34.56.78 == A record (IPv4)

example.com => AWS resource == Alias (ex: ELB, CloudFront, S3, RDS, etc…)


Domain registration

DNS

Health Checks

Routing Policies


**Has different routing policies:**

Simple Routing Policy

Weighted Routing Policy

Latency Routing Policy

Failover Routing Policy

Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. It is designed to give developers and businesses an extremely reliable and cost-effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other.

Weighted routing lets you associate multiple resources with a single domain name (example.com) or subdomain name (acme.example.com) and choose how much traffic is routed to each resource. This can be useful for a variety of purposes, including load balancing and testing new versions of software. To configure weighted routing, you create records that have the same name and type for each of your resources. You assign each record a relative weight that corresponds with how much traffic you want to send to each resource. Amazon Route 53 sends traffic to a resource based on the weight that you assign to the record as a proportion of the total weight for all records in the group.

Route 53 Routing Policy Overview:

![[route-53-routing-policies.jpg]]


# CloudFront


Content Delivery Network (CDN)

improve read performance, content is cached at the edge

Fast loading because it is cached


Use cases:

S3 bucket 
-> for distributing files and caching them at the edge
-> for uploading files to S3 through CloudFront
-> secured using Origin Access Control (OAC)

Generates a bucket policy for you


VPC origin

-> For apps hosted in VPC private subnets
-> Private app load balancer / network load balancer / ec2 instances

Custom Origin (HTTP)

-> S3 website (enable bucket as a static S3 website)
-> Public HTTP backend like public ALB

Cloud Front uses theses services to protect against web attacks:

AWS WAF -> helps protect your applications by filtering malicious web traffic

AWS Shield ->  provides advanced DDoS protection, working together to enhance your application security against web attacks.



#  S3 Transfer Acceleration

Increase transfer speed by transferring file to an AWS edge location which will forward the data to the S3 bucket in the target region

use case:

transfer files from all around the world into one specific S3 bucket

# Global Accelerator

Improves global application availability and performance (increased to 60%)


![[Screenshot 2026-02-09 224116.png]]

in your region, clients can go through a lot of hops an a lot of network and there could be problems and there could be latencies added to it.

Using the global acclerator  you just connect to an edge location of AWS and then quickly from the edge location to the region you are connecting to, it goes through the private AWS network which is much more faster

No caching -> proxing packages at the edge to the applications running in one or more AWS region 

# Outposts

Servers within your premises infrastructure

They are server racks that offers the same AWS infrstucture, services, APIs & tools to build your own applications on-premises just as in the cloud

Outposts racks are directly setup by AWS

You are responsible for the physical security

Benefits:

Low-latency access to on-premises

local data processing -> so the data may actually never leave your on-premise system and never go to cloud

Data residency -> lives within your own data centers

Easier migration from on-premises to the cloud

Fully managed service -> you dont need to manage the servers

Services used by Outposts:
EC2 ,EBS, S3, EKS, ECS, RDS, EMR

# WaveLength Zones

AWS deployment designed specifically for edge computing on 5G networks

Embed AWS compute and storage services directly within the data centers of telecommunications providers, at the edge of their 5G networks, this includes EC2, EBS, VPC


Ultra-low latency applications from 5G networks


no additional charges

Use cases: smart cities, machine learning diagnostics, connected vehicles, interactive live streaming, real time gaimng


# Local Zones


The ability to place compute storage database and other services closer to end users

especially good for running latency-sensitive apps

Essentially you are extending your AWS region to one or more locations, availability zones one or more


![[Screenshot 2026-02-11 131839.png]]



### **Quick Comparison Table**

| Feature                  | Availability Zone (AZ)                   | Local Zone (LZ)                                         |
| ------------------------ | ---------------------------------------- | ------------------------------------------------------- |
| **Geographic placement** | Within the Region’s main metro area      | In a different, often distant, metro area               |
| **Proximity to users**   | Regional                                 | Close to specific user populations                      |
| **Latency to end‑users** | Higher (if user is far from Region)      | Very low (single‑digit ms) for local users              |
| **AWS services offered** | Full AWS service catalog                 | Limited subset (primarily compute, storage, networking) |
| **Typical use case**     | General‑purpose HA and scalability       | Ultra‑low‑latency edge workloads                        |
| **Management**           | Native to Region, fully integrated       | Extended part of a Region, same APIs/VPC                |
| **Fault isolation**      | Designed to be independent within Region | Dependent on parent Region for some services/management |
### **Key Takeaway**

- **AZs** are the standard building blocks for resilient cloud architecture **within a Region**.
    
- **Local Zones** bring AWS infrastructure **to the edge** – they are AZ‑like but placed in specific metros to serve workloads that cannot tolerate the latency of a distant Region.

# Global Applications Architecture

## Single Region, Single AZ


We have an EC2 instance in one easy in one region that does not give us high availability, for sure.

Low availabilty -> This does not give us good global agency, because if we access this institution from a user that's very, very far away

Bad  latency -> from a region is going to get bad at latency. And it's very, very simple to set up.

Easy -> very low difficulty.


![[Screenshot 2026-04-03 221620.png]]
## Single region, Multi AZ

2 AZs within one region

High Availability -> Has high availability

Bad Latency ->  high latency

easy - Medium diffucluy ->  difficulty increased a bit


![[Screenshot 2026-04-03 215656.png|424]]



## Multi Region, Active Passive


Active passive means 2 regions, each region has one or multiple AZs and in one region our EC2 instances will be active or application will be active

Active
Users can do reads and writes to their EC2 wherever they are in the world, in the active region

Passive
The other EC2 is passive, meaning there is data replication between the active region and the passive region. Users can do reads from the passive region, but not writes the passive region

if we have all regions of the world and they are passive -> means improved read latency


because now we have our data replicated
across the world and with low latency,
but for writes well, all the writes still need to go
to the same central region.
So that means that the writes at a global level


Good Global reads latency

No Global writes latency

moderate difficulty


![[Screenshot 2026-02-11 174141.png]]


## Multi Region, Active - Active

Each EC2 instance is able to write and reads, replication still happens within the 2 instances -> improving read  and write latency

Higher difficulty -> your application has to do alot of things in every single region, more difficult to setup

Use casess:

database having an active-active demo setup is dynamoDB  Global tables

![[Screenshot 2026-02-11 175850.png]]


# Quiz

Question 1:

Which Route 53 Routing Policies would you use to route traffic to multiple resources in proportions that you specify?

The Weighted Routing Policy is correct because it allows you to distribute traffic across multiple resources based on specified proportions, making it ideal for balancing loads or testing new features. This understanding aligns well with the learning objective of recognizing which routing policy serves multiple resources effectively.



Question 2:

Which service is optimized to deploy ultra-low latency applications to 5G devices?

WaveLength

Question 3:

You need to enable fast, easy, and secure transfers of files over long distances on S3. Which service would you use?

S3 Transfer Acceleration

Question 4:
What does AWS CloudFront use to improve read performance?

Caching content in edge locations

CloudFront uses Edge Location to cache content, and therefore brings more of your content closer to your viewers to improve read performance

Question 5:

Which service can be used to run AWS infrastructure and services on-premises for a hybrid cloud architecture?

Outposts 
Brings native AWS services, infrastructure, and operating , models to virtually any data center, co-location space, or on-premises faculty 

Question 6:
Which of the following statements is NOT a reason for a global application?

Scale elasticity on demand
A global application is not specifically used to scale elastically on demand. You can use Auto Scaling Groups for example if you want to elastically scale based on demand


Question 7:
Which features are available with Route 53?

Domain Registration, DNS, Health Checks, Routing Policy


Question 8:

With which services does CloudFront integrate to protect against web attacks?

WAF & Shield