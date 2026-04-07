

Amazon EC2

Elastic Compute Cloud this is a Infrastructure as a service, involves renting of virtual machines 


EC2 offers configuration options like:

- OS,  How much CPU, RAM, Storage, Network card, firewalls (security groups), Bootstrap script


What is a bootstrap script (user data script)?


A script that runs only once at the instance  first start. Launching of commands when a machine starts. User data is is used to automate boot tasks such as, installing update, softwares, downloading files from the internet

EC2 user data script runs with the root user


## Launching a new EC2 Instance

Click on instances

![[creatingInstance1 2.png]]

-------------------------------------------------------------------------
Click on launch instances

![[creatingInstance2.png]]


--------------------------------------------------------------------------

Get to instance page

![[creatingInstance3.png]]

-----------------------------------------------------------------------
Write a name for your instance

![[creatingInstance4.png]]


-------------------------------------------------------------------------------

Choose Amazon Linux 2 AMI so it can be in free tier

![[creatingInstance5.png]]![[creatingInstance6.png]]![[creatingInstance7.png]]



--------------------------------------------------------------------------

Choose an instance type, they differ based on the number of CPUs, memory and cost they have. t2.micro is selected this one is free tier for a month. You can scroll to see more options

![[creatingInstance9.png]]

![[creatingInstance10.png]]

------------------------------------------------------------------------

You need to create a key pair to login to your instance using SSH

![[creatingInstance11.png]]

Click on this to create a new key pair

![[creatingInstance12.png]]

You get this pop up to create a new key pair. Write the name of the key pair, select RSA for the type, and select .pem for the format since we will be using windows 10, Mac or Linux. Click create to download the key pair.

![[creatingInstance13.png]]

----------------------------------------------------------------------

For now we don't need to touch anything. make sure your Auto-assign public IP is enabled

![[creatingInstance14.png]]

This security group attached to our instance, is going to control the traffic from and to our instance, therefore we can add rules.

The first security group created will be called launch-wizard-1

![[creatingInstance15.png]]


We can define multipe rule directly on the console. Our first one we can allow SSH traffic from anywhere

We also want to allow HTTP traffic from the internet, so we tick it

For now we don't need to tick the HTTPS

![[creatingInstance16.png]]


--------------------------------------------------------------------------


Configure storage we could leave it like this to be free tier. Only one volume is necessary

![[creatingInstance17.png]]

You can click on Advanced to see more details. Once the EC2 is terminated the volume will be deleted 

![[creatingInstance18.png]]

-------------------------------------------------------------------------------------------------------------

These are the advanced details we can leave as is for now but we want to look at User Data at the bottom

![[creatingInstance19.png]]



User data is when we pass a script, to execute at first launch of our EC2 instance![[creatingInstance20.png]]

Here it is with a script, and will be executed when the instance is first started and only once

The scrip will 

update a few things

install HTTPD web server on the machine

then write a html file that will be our web server
 
 ![[creatingInstance21.png]]
 
-------------------------------------------------------------------------------------------------------------

Take a look at summary to review, and launch instance

![[creatingInstance22.png]]

--------------------------------------------------------------------------

Now we could see the instance in instances dashboard 

![[creatingInstance23.png]]


-------------------------------------------------------------------------

## Taking a look at the web server

Copy the Public IPv4 address or click on open address


![[accessingInstance1.png]]


For this case make sure it is HTTP not HTTPS for the url since we made the HTTPS private

![[accessingInstance2.png]]

if there is a timeout it is likely caused by an EC2 security group

------------------------------------------------------------------------

## Inbound Rules

An inbound rule specifies **which types of traffic are allowed to enter** a resource, based on criteria like protocol, port range, and source IP or security group



![[inboundRules.png]]

HTTP is port 80  automatically   

SSH is port 22 automatically

HTTPS is port 443 automatically


### 🔸 1. **HTTP (Port 80)**

- **Protocol:** TCP
    
- **Purpose:** Used for **unencrypted web traffic**.
    
- **Common Use:** When users visit a website using `http://your-domain.com`, their browser connects to your server on port 80.
    
- **Source:** `0.0.0.0/0` — allows anyone on the internet to access your web server.
    
- **Risk:** Open to the world; acceptable for public web servers, but not for private/internal apps.
    

---

### 🔸 2. **SSH (Port 22)**

- **Protocol:** TCP
    
- **Purpose:** Used for **Secure Shell (SSH)** connections to remotely manage your Linux-based instance.
    
- **Common Use:** You connect via a terminal (e.g., `ssh ec2-user@<instance-ip>`) for administrative access.
    
- **Source:** `0.0.0.0/0` — means **anyone** can attempt to SSH into your instance.
    
- ⚠️ **Security Warning:** This is risky.  
    It’s best practice to **restrict SSH access** to your own IP (e.g., `203.0.113.25/32`) instead of leaving it open to the world.
    

---

### 🔸 3. **HTTPS (Port 443)**

- **Protocol:** TCP
    
- **Purpose:** Used for **secure, encrypted web traffic**.
    
- **Common Use:** When users visit your website using `https://your-domain.com`, communication happens over port 443 with SSL/TLS encryption.
    
- **Source:** `0.0.0.0/0` — allows anyone to securely access your website.
    
- **Good Practice:** Safe and expected for public-facing web servers.


----------------------------------------------------------------

## Outbound Rules


An outbound rule specifies **which types of traffic are allowed to leave** your AWS resource, based on the destination IP address or range, port, and protocol.

**Only outbound data transfer is charged**
### 🔹 **Example Use Cases**

- Allow EC2 instance to **access the internet** (software updates, APIs, etc.).
    
- Allow EC2 instance to **communicate with a database** in a private subnet.
    
- Restrict outbound traffic to **specific destinations or ports** for security (e.g., only port 443 for HTTPS).

### 🔹 **Example: EC2 Security Group Outbound Rule**

|Type|Protocol|Port Range|Destination|
|---|---|---|---|
|All traffic|All|All|0.0.0.0/0|

**Meaning:**

- The EC2 instance can **send any kind of traffic** (HTTP, HTTPS, SSH, etc.)  
    to **any IP address on the internet**.

----------------------------------------------------------------------

## Inbound vs. Outbound Rules

| Direction    | Controls                             | Example                                | Default Behavior                            |
| ------------ | ------------------------------------ | -------------------------------------- | ------------------------------------------- |
| **Inbound**  | Traffic **coming into** the instance | Allow HTTP (port 80) from anywhere     | **No inbound traffic** allowed by default   |
| **Outbound** | Traffic **leaving** the instance     | Allow all outbound traffic to anywhere | **All outbound traffic** allowed by default |


## EC2 Instance Purchasing options 

![[ec2-pricing-plans.jpg]]


### On-Demand Instances

an instance that you use on-demand. You have full control over its lifecycle — you decide when to launch, stop, hibernate, start, reboot, or terminate it. There is no long-term commitment required when you purchase On-Demand Instances. There is no upfront payment and you pay only for the seconds that your On-Demand Instances are running. The price per second for running an On-Demand Instance is fixed. On-demand instances cannot be interrupted.

Pay for what you use, billing per second after first minute (only linux or window)

Has highest cost

No long-term commitment

Recommended for short-term and un-interrupted workloads, where you can't predict how the application will behave

***coming and staying in resort** **whenever we like, we pay the full price***
###  Reserved Instances

provides you with significant savings on your Amazon EC2 costs compared to On-Demand Instance pricing. Reserved Instances (RI) are not physical instances, but rather a billing discount applied to the use of On-Demand Instances in your account. You can purchase a Reserved Instance (RI) for a one-year or three-year commitment, with the three-year commitment offering a bigger discount. You will be charged for the entire duration, irrespective of your usage.


Reserved instances are used for steady-state usages like for databases. You  reserve a specific attributes and specify a reservation period

Discounted pricing compared to On-demand (72% discount)

You reserve a specific instance attributes (Instance Type, Region, Tenancy, OS)

Specify a reservation period 1yr (discounted) or 3 yrs (discounted +)

Multiple payment options: Non upfront (discounted), Partial Upfront (discounted +), All Upfront (discount ++)

Scope of reserved instance (i.e. Do you want the scope to be into a specific region or a zone) 

You can buy or sell your reserved instances to a marketplace if you don't need them anymore


Convertible Reserved Instance

A reserved instance that can be changed (instance type, instance family, OS, scope, and tenancy)
lesser discount compared to regular

***like planning ahead and if we plan to stay for a long time, we may get a good discount.***


### Savings Plans


Get a large discount based on long term usage (up to 72% same as Reserved Instance). You must commit to a certain type of usage (i.e. $10/hour for 1 or 3 years) and you are locked to a specific instance family & AWS region (i.e. M5 in us-east-1)

Flexible across instance size, OS, and Tenancy (Host, Dedicated, Default)

***pay a certain amount per hour for certain period and stay in any room type (e.g., King, Suite, Sea View, …)***
### Spot Instances 

an unused EC2 instance that is available for less than the On-Demand price. Because Spot Instances enable you to request unused EC2 instances at steep discounts, you can lower your Amazon EC2 costs significantly. Spot Instances are well-suited for data analysis, batch jobs, background processing, and optional tasks. These can be terminated at short notice, so these are not suitable for critical workloads that need to run at a specific point in time.


Large discount (up to 90%) compared to On-Demand. The most cost-efficient instances. However you can lose this instance at any point if your max price is less than the current spot price.

Most useful for workloads that are resilient to failure (i.e. batch jobs, data anylsis, image processing, distributed workloads, flexible workloads)

DONT USE this for critical jobs or databases

***the hotel allows people to bid for the empty rooms and the highest bidder keeps the***
***rooms. You can get kicked out at any time***


### Dedicated Hosts

Amazon EC2 Dedicated Host allows you to use your eligible software licenses from vendors such as Microsoft and Oracle on Amazon EC2 so that you get the flexibility and cost-effectiveness of using your licenses, but with the resiliency, simplicity, and elasticity of AWS. An Amazon EC2 Dedicated Host is a physical server fully dedicated for your use, so you can help address corporate compliance requirement. A Dedicated Host is not cost-efficient compared to an On-Demand instance.


A physical server with EC2 instance capacity fully dedicated to your use. For companies that have complex licensing, or regulations

Allows you to address compliance requirements  (rules, regulations, organizational standards to ensure legal, ethical accountabilities) and software licenses

Purchasing options

- On-demand: pay per sec

- Reserved: pay 1 or 3 yrs Non upfront (discounted), Partial Upfront (discounted +), All Upfront (discount ++)

Most expensive


***We book an entire building of the resort***
### Dedicated Instances

Instances run on hardware that's dedicated to you. These may share hardware with other instances in the same account. Just like dedicated host it allows visibility for the lower level hardwares


You can't control/choose the instance placement.  you do not have control over the specific physical server on which your instances are placed


In the context of AWS Dedicated Instances, "No control over instance placement (can move hardware after Stop/Start)" means that while Dedicated Instances ensure that your instances run on hardware that is dedicated to your account (not shared with other customers), you do not have control over the specific physical server on which your instances are placed. ​

When you stop and then start a Dedicated Instance, AWS may move the instance to a different physical server within the same availability zone. This is because AWS manages the underlying infrastructure and optimizes resource allocation. ​ Unlike Dedicated Hosts, where you have control over the physical server placement, Dedicated Instances do not provide this level of control. ​


### Capacity Reservations

Reserve On-Demand instances capacity in a specific AZ for any duration. No time commitment (cancel anytime), but no billing discounts.

The only purpose is to reserve capacity, which is good for short term uninterrupted workloads that needs to be in a specific AZ
 - Capacity Reservations are ideal for scenarios where you need guaranteed compute capacity in a specific AZ for a limited period. (useful for applications that need to be live (like live stream) and require specific AZ)


For example, you are hosting a live-streaming event and need to ensure that your EC2 instances are available in **us-east-1a** to handle the expected traffic spike. You can use **Capacity Reservations** to reserve the required number of EC2 instances in **us-east-1a** ahead of time, ensuring that the capacity is available when you need it.


***you book a room for a period with full price even you don’t stay in it***




## EC2 Instance Purchasing Options Comparison

| **Option**                         | **Description**                                                                             | **Billing / Cost**                                                                                | **Commitment**                     | **Flexibility**                                                                     | **Best For**                                                                   | **Risks / Drawbacks**                                               | **Analogy**                                                                            |
| ---------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ---------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| **On-Demand Instances**            | Pay per second (after first minute) for compute capacity. No need to plan or reserve.       | 💰 Highest cost. Pay only for what you use.                                                       | ❌ None                             | ✅ Full flexibility in instance type, region, etc.                                   | Short-term, unpredictable, or testing workloads.                               | Most expensive option long term.                                    | 🏖 _Coming and staying in a resort whenever we like, paying full price._               |
| **Reserved Instances (Standard)**  | Reserve specific instance attributes for 1 or 3 years at a discount.                        | 💵 Up to 72% cheaper than On-Demand. Multiple payment options (No Upfront, Partial, All Upfront). | ✅ 1 or 3 years                     | ❌ Tied to specific instance type, region, OS, and tenancy.                          | Steady-state workloads (e.g., databases).                                      | Less flexible; locked to chosen configuration.                      | 🏨 _Planning ahead and staying long-term for discounts._                               |
| **Convertible Reserved Instances** | Same as Reserved Instances but can change attributes (type, family, OS, tenancy).           | 💵 Slightly smaller discount than Standard RI.                                                    | ✅ 1 or 3 years                     | ⚙️ More flexible than Standard RI.                                                  | Long-term workloads needing some adaptability.                                 | Still requires time commitment.                                     | 🔁 _Plan ahead, but can change room type later._                                       |
| **Savings Plans**                  | Commit to a consistent amount of usage ($/hr) for 1 or 3 years in exchange for lower rates. | 💸 Up to 72% discount (similar to RI). Pay based on usage commitment.                             | ✅ 1 or 3 years                     | ⚙️ Flexible across instance size, OS, tenancy, and region (depending on plan type). | Consistent workloads with predictable spend.                                   | Locked to usage commitment; overcommitment wastes money.            | 🏩 _Pay a fixed amount per hour and stay in any room type (King, Suite, Sea View...)._ |
| **Spot Instances**                 | Use spare EC2 capacity with variable pricing. Can be interrupted anytime.                   | 💰 Up to 90% cheaper than On-Demand.                                                              | ❌ None                             | ⚙️ Flexible, but not reliable.                                                      | Batch processing, AI training, non-critical or fault-tolerant workloads.       | Instances can be terminated without notice. Not for critical tasks. | 🎯 _Bid for empty hotel rooms — you may get kicked out anytime._                       |
| **Dedicated Hosts**                | Physical server fully dedicated to you. Useful for compliance and licensing.                | 💰💰 Most expensive option. Available On-Demand or Reserved (1/3 years).                          | ✅ Optional (On-Demand or Reserved) | ❌ Limited flexibility. Full hardware control.                                       | Compliance-heavy workloads, legacy licensing, or strict security requirements. | High cost; overprovisioning risk.                                   | 🏢 _Booking an entire resort building for yourself._                                   |
| **Dedicated Instances**            | Instances run on hardware dedicated to your AWS account (shared within account).            | 💵 Higher than On-Demand.                                                                         | ❌ None                             | ⚙️ Moderate — hardware is dedicated, but AWS controls placement.                    | Workloads needing isolated hardware but not full control.                      | No control over physical placement; may move after Stop/Start.      | 🏠 _Have a private villa, but can’t choose its exact spot._                            |
| **Capacity Reservations**          | Reserve On-Demand capacity in a specific Availability Zone.                                 | 💸 Pay On-Demand rates (no discount).                                                             | ❌ None (cancel anytime)            | ⚙️ Can combine with RI or SP for savings.                                           | Short-term or event-based workloads needing guaranteed capacity.               | No pricing discount; pay even if unused.                            | 🪑 _Book a room and pay full price even if you don’t stay in it._                      |


### ✅ Quick Summary

- **Most Flexible:** On-Demand
    
- **Most Cost-Effective:** Spot (if non-critical)
    
- **Best for Predictable Use:** Reserved or Savings Plan
    
- **Best for Compliance/Control:** Dedicated Host
    
- **Guaranteed Availability:** Capacity Reservation


## Shared Responsibility Model for EC2

### AWS Responsibilities:

Infrastucture, global network secruity

Isolation on physical hosts (ensure that virtual machines (EC2 instances) running on the same physical server are securely isolated from one another.)

Replacing faulty hardware

Compliance validation

### You:

Security Groups rules

Operating-system patches and updates ->  

**Managing patches of the guest operating system on Amazon Elastic Compute Cloud (Amazon EC2)**



Software and utilities installed on the EC2 instance

IAM Roles assigned to EC2 & IAM user access management

Data security on your instance

