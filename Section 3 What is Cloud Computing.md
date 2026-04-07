## What is Cloud Computing?

Cloud Computing is  the On-Demand Availability of computer system resources, especially data storage (cloud storage) and computing power, without direct active management by the user

What does this definition mean?

**On-Demand Availability** -> means  you can access resources (like storage, servers,  or applications) whenever you need them. Resources are provisioned almost instantly

**Without Direct Active Management by the User** -> Amazon Web Services owns and maintains the network-connected hardware required for these application services, while you provision and use what you need via a web application

In other words: Cloud computing is the on-demand delivery of compute power, database storage,
applications, and other IT resources


## The Deployment Models of the Cloud

**Private Cloud**
Cloud services used by single org, not exposed to public. Security for sensitive applications

**Public Cloud**
Cloud resources owned/operated by 3rd party cloud service provider. Has *6 advantages of Cloud Computing* 

**Hybrid Cloud** 
Some servers on premises and extend some capabilities to the cloud. Allows you to benefit from the flexibility, scalability, and on-demand storage access while keeping security and performance


## 5 Characteristics of Cloud Computing

### 1. On-demand self service**
Users can provision resources and use them without human interaction from the service provider
	
-> On-Demand -> you get resources whenever you need them, instantly

-> Self service -> users themselves can request configure through a web portal

-> No human interaction from the provider -> No need a technician, process is automated, instantly allocates requested storage, server, or app

### **2. Broad Network access**
Resources available over the network, and can be accessed by diverse client platforms

-> Resources available over the network -> Cloud services are delivered through the internet, just need internet connection

### **3. Multi-tenancy and resource pooling**
Multiple customers can share the same infrastructure and applications with security and privacy 
Multiple customers are serviced from the same physical resources

-> This means not just us can share the same AWS while having security and privacy

### **4. Rapid elasticity and scalability**
Automatically and quickly acquire and dispose resources when needed. Quickly and easily scale based on demand

-> Elasticity means ->  the cloud's ability to automatically provision and de-provision resources in real-time based on current traffic. When traffic spikes, it adds more servers; when traffic drops, it shuts them down

-> Scalability means -> the ability of your system to handle increased load by making longer-term changes, like upgrading to a more powerful server (vertical) or adding more servers to your pool (horizontal).

### **5. Measured service**
Usage is measured, users pay correctly for what they have used

## 6 Advantages of Cloud Computing

### 1. Trade capital expense for operational expense (variable expense)

Pay On-Demand -> don't own hardware

Reduced Total Cost of Ownership (TCO) & Operational Expense (OPEX)
-> don't buy hardware in advance, it is just like renting it from AWS

### 2. Benefit from massive economies of scale

Prices are reduced as AWS is more efficient due to large scale
-> Microsoft, Amazon and Google are so enormous in global scale (millions of servers, huge data centers) they achieve efficiencies that make services cheaper for everyone


**Simple analogy:** A giant like Walmart can sell a soda for less than the corner store because it buys a million cans at once, has ultra-efficient logistics, and shares overhead costs across thousands of stores. The corner store buys 100 cans, has higher per-unit costs, and has to charge more.

Cloud providers are the "Walmart of computing," and we all get the benefit of their low prices.

The chain reaction (out of scope for the certificate lol)

→ **Leads to Enormous Physical Scale** (millions of servers, huge data centers)  
→ **Which Creates Unbeatable Operational Efficiencies** (buying power, optimized hardware, full utilization)  
→ **Which Drives Down Their Cost to Provide Each Unit of Service**  
→ **Which Allows Them to Offer Lower Prices to Customers**

### 3. Stop guessing capacity
Scale based on actual measured usage
-> no need to plan your pricing, it is automatic
### 4. Increase speed and agility
-> We can create and operate immediately , no blockers that block efficiency

### 5. Stop spending money running and maintaining data centers
-> avoids huge costs

### 6.  Go global in minutes: leverage the AWS global infrastructure 
-> allows a team of 5 people to create a global application in minutes


![[pt4-q45-i1.jpg]]

## Problems solved by the Cloud

**Flexibility**
Change resource types when needed

**Cost-Effectiveness**
Pay as you go, for what you use

**Scalability**
accommodates larger loads by making hardware stronger of adding additional nodes
-> add more as you needed

**Elasticity**
Ability to scale out and scale-in when needed

**High-availability and fault-tolerance**
build across data centers
-> don't rely on one data center, rely on a fleet of data centers

**Agility**
rapidly develop, test and launch software applications


## Types of Cloud Computing

### Traditional On-Premises IT (not considered cloud computing)

You manage: Apps, data, runtime, middleware, o/s, virtualization, servers, storage, network
AWS manages: Nothing

### Infrastructure as a Service (IaaS)
The building blocks for Cloud IT, provides networking, computers, data storage space. It has the highest level of flexibility and easily parallels with tradition on-premises IT

You manage: Applications, Data, Runtime, Middleware, O/S

AWS manages: virtualization, servers, storage, network

Examples: Amazon EC2, GCP, Azure

### Platform as a Service (PaaS)
Removes the need for your organization to manage the underlying infrastructure. Focusses on the deployment and management of your applications

You manage: Applications and Data

AWS manages: runtime, middleware, o/s, virtualization, servers, storage, network

Examples: Elastic Beanstalk, Heroku, Google App Engine (GCP), Windows Azure (Microsoft)
### Software as a Service (SaaS)
Completed product that is run and managed by the service provider

You manage: Nothing

AWS manages: Apps, data, runtime, middleware, o/s, virtualization, servers, storage, network

Examples: Many AWS services like Rekognition for Machine learning, Google Apps (Gmail), Dropbox, Zoom


## Pricing of the Cloud 

Uses the *pay as you go* pricing model based on 3 fundamentals:

**1. Compute** 
Pay for compute time

**2. Storage**
Pay for data stored in the Cloud

**3.  Networking**
Pay for Data transfer OUT (leaves the Cloud) of the Cloud
-> Data transfer INTO the Cloud is FREE

Solves the expensive issue of traditional IT since we only pay what we need


## AWS Global Infrastructure


Regions  ->  Contains  -> Availability Zones  -> Contains -> Data Centers


### 1. AWS Regions 

Each region has many Availability Zones. They are a cluster of data centers. AWS has regions all around the world and most AWS service are **Region-Scoped** 

Names can be us-east-1, eu-west-3…

#### How to choose an AWS Region?

Factors that may impact your choice

##### Compliance with data governance and legal requirements
Data never leaves a region without your explicit permission
-> data in France may have to stay in france

##### Proximity to customers
reduced latency
-> If you deploy your application in Australia and you users are in America, they will have a lot of lag

##### Available Services within a region
new service and new features aren't available in every Region
-> You need to make sure that the region you're deploying into is available and has that service


##### Pricing
pricing varies region to region and is transparent in the service pricing page


### 2. AWS Availability Zones

Each AZ is one or more discrete data centers with redundant power, networking, and connectivity

They are separate from each other, to isolate from disasters

Connected with high band ultra low latency networking, therefore linking together data centers of AZs to form a region

Written like at the end of the region, like so:
• ap-southeast-2a
• ap-southeast-2b
• ap-southeast-2c


### 3. Data Centers

#### Point of Presence
An **Edge Location** is a small data center owned by AWS

Its **only job** is to cache (keep a temporary copy of) static content from your main server and deliver it to users who are geographically close to it. They are strategically placed to be as close as possible to the end-users.

Content is Delivered with Lower Latency



## Shared Responsibility Model

**AWS is responsible for securing the cloud infrastructure. You are responsible for securing anything you put on that infrastructure.** Understanding where that line is drawn for each service you use is the key to building secure applications in the cloud.