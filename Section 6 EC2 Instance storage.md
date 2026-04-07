
# Elastic Block Store (EBS) Volume 

A network drive you can attach to your instances while they run

Uses the network to communicate the instance, so there might be latency

it can detach from an EC2 instance and attach to another one quickly -> can be attached on demand

Locked to one Availability zone (AZ), you need to take a snapshot first

You must provision the capacity in advance, you get billed and could increase it over time


## Delete on Termination 

controls the EBS behavior when an EC2 instance is being terminated.

Root volume
- By default it is ticked for the root volume, the EBS volume is DELETED alongside the instance being terminated. So it's enabled.

Any other attached EBS volume 
- is NOT DELETED because it's disabled by default.

Use cases

if you want to preserve the root volume when an instance is terminated, for example to save some data, then you can disable delete on termination for the root volume and you'll be good to go.

# EBS Snapshots

snapshot is a backup of your EBS volume at a point in time

Highly recccomended but not mandatory when detaching a volume

Can copy snapshots across AZ or regions

## Archive

move a Snapshot to an archive tier -> 75% cheaper

can be restored

## Recycle Bin

You can setup recycle bin to keep deleted snapshots and recover them


# Amazon Machine Image (AMI)

Customization of an EC2 -> add your own configs

Faster boot . config time since it is prepackaged

built for specific regions


**You must use an Amazon Machine Image (AMI) from the same region as that of the Amazon EC2 instance. The region of the Amazon Machine Image (AMI) has no bearing on the performance of the Amazon EC2 instance**

An Amazon Machine Image (AMI) provides the information required to launch an instance. You must specify an Amazon Machine Image (AMI) when you launch an instance. You can launch multiple instances from a single AMI when you need multiple instances with the same configuration.

The Amazon Machine Image (AMI) must be in the same region as that of the Amazon EC2 instance to be launched. If the Amazon Machine Image (AMI) exists in a different region, you can copy that Amazon Machine Image (AMI) to the region where you want to launch the EC2 instance. The region of Amazon Machine Image (AMI) has no bearing on the performance of the Amazon EC2 instance.


![[pt3-q34-i1.jpg]]

Can launch EC2 from

public AMI

own AMI

an AWS marketplace AMI -> saves time

AWS Marketplace offers two ways for sellers to deliver software to customers: Amazon Machine Image (AMI) and Software as a Service (SaaS).

Amazon Machine Image (AMI): Offering an AMI is the preferred option for listing products in AWS Marketplace. Partners have the option for free or paid products. Partners can offer paid products charged by the hour or month. Bring-Your-Own-License (BYOL) is also available and enables customers with existing software licenses to easily migrate to AWS.

Software as a Service (SaaS): If you offer a SaaS solution running on AWS (and are unable to build your product into an AMI) the SaaS listing offers our partners a way to market their software to customers.
![[Screenshot 2026-02-24 150502.png]]


# Image Builder

Used to automate the creation of Virtual Machines or container images

You can automate the creation, maintain, validate and test EC2 AMIs

Free service, but pay for the created EC2 instances and AMI storage, whatever is created with the builder

1. EC2 Image builder
	1. creates an EC2 instance called Builder EC2 instance
	2. Can be run on a schedule or whenever packages are updated, or manually
2. Builder EC2 Instance
	1. Builds components, and customize software, like install Java, update CLI, update software, install firewalls, etc.
	2. New AMI is created
3. New AMI
	1. EC2 Image builder automatically creates a test EC2 instance from this AMI and run tests for validation
	2. Once tests are passed, AMI is ready to be distributed to multiple regions



![[Screenshot 2026-02-24 152200.png]]


# Instance Store

EC2 Instance store has higher performance than normal EC2 instance,  a hard disk space that is attached directly

EC2 instance store, Good for buffer / cache/ scratch data/ temporary content, but risk of data loss if hardware fails

EC2 instance store lose their storage if they're stopped ephemeral


# Elastic File System EFS


you can attach onto an EC2 instance. And this is a network file system or NFS. EFS stands for elastic file system and it is a managed network file system.

 before we had an EBS volume attached to only one EC2 instance at a time. But with an EFS drive, you can mount it onto hundreds of EC2 instances.

The benefits -> it can be mounted to hundreds of EC2 instances at a time.






![[Screenshot 2026-02-25 164122.png]]



We have an EFS file system with a security group, and then we have EC2 instances in various availability zones connected to it.

So, we have EC2 instances in us-east-1a, EC2 instances in us-east-1b, as well as EC2 instances in us-east-1c.

And they're all connected to the same EFS File system.

----------------------------------

![[Screenshot 2026-02-25 165016 1.png]]


So, with EBS, say we had EC2 instance in one AZ and another one. Then the EBS volume can only be attached to one instance in one specific AZ. And the EBS volumes are bound to specific availability zones.

But if we wanted to move over the EBS volume from one AZ to another, we could create a snapshot, it would create an EBS snapshot and then restore that snapshot into a new availability zone. And effectively we would've moved the EBS volume over.

But this is a copy, this is not an in-sync replica. This is a copy, and that would mean that this drive can now be used by another EC2 instance.




-------------------------------

![[Screenshot 2026-02-25 165940.png]]




EFS is a network file system. That means that whatever is on the EFS drive is shared by everything that is mounted to it.

So, what does that mean?

Say we have many instances in Availability Zone 1 on one or many instances as well on Availability Zone 2. At the same time, all these instances can mount the same EFS drive, okay, using a mount target, and they will all see the same files.

So, that makes it a shared file system.

## EFS Infrequent Access (EFS-IA)

Storage class that is cost-optimized for files not accessed every day

EFS will automatically move your files to EFS-IA based on the last time they were accessed


# Shared Responsibility Model for EC2 Storage

AWS responsibilities
- Infrastructure
- Replications for EBS volumes & EFS drives
- Replacing faulty hardware
- Employees not having access to your data

Your responsibility
- Setting up backup/ snapshot procedures
- setting up data encryption
- responsibility of any data on the drive
- understand risks of ec2 instance store


# FSx

a third party high performance file system on AWS, fully managed service

Offerings:
- FSx for Lustre
- FSx for windows File Server
- FSx for NetApp ONTAP


## Windows File Server

A fully managed, scalable windows native shared file system

Windows instances

Usually for deploying  FSx across 2 availability zones

Has support for all windows native protocols -> allowing you to mount this FS to your windows machines
- SMB protocol
- Windows NTFS

Having EC2 instances that are windows based they could access windows file server

Can be accessed from AWS or on-premise


![[Screenshot 2026-02-27 135920.png]]

## Lustre

A scalable file storage for high performance computing

Linux and Cluster

scales up to 100s GB/s, millions of IOPS, sub-ms latencies

Usages: Machine Learning, Analytic Video Processing, Financial Modeling


![[Screenshot 2026-02-27 135823 1.png]]



So the way it works is that Amazon FSx for Lustre can be connected either to your corporate data center or to your compute instances directly within AWS. And then in the backend, Amazon FSx for Lustre is actually storing your data, possibly onto an Amazon S3 bucket.



# Storage Comparisons


|**Feature**|**Amazon EBS (Elastic Block Store)**|**Instance Store (Ephemeral Storage)**|**Amazon EFS (Elastic File System)**|**Amazon FSx**|
|---|---|---|---|---|
|**Type**|Persistent block storage (like a virtual hard drive)[](https://awstip.com/unlocking-aws-ec2-storage-a-complete-guide-to-ebs-efs-instance-store-526e74e8e06d?gi=46bff44d1149&source=collection_home---4------1-----------------------)|Temporary, block-level storage physically attached to the host server[](https://docs.aws.amazon.com/en_us/AWSEC2/latest/UserGuide/Storage.html)|Scalable, fully-managed file storage[](https://dev.to/kouta222/aws-storage-services-comparison-s3-ebs-efs-and-fsx-4nm0)|Fully-managed, specialized, high-performance file systems[](https://dev.to/kouta222/aws-storage-services-comparison-s3-ebs-efs-and-fsx-4nm0)|
|**Persistence**|Data persists independently of an EC2 instance's lifecycle, surviving stop, terminate, or hardware failure[](https://docs.aws.amazon.com/en_us/AWSEC2/latest/UserGuide/Storage.html)|Data is lost if the EC2 instance is stopped, hibernated, or terminated[](https://docs.aws.amazon.com/en_us/AWSEC2/latest/UserGuide/Storage.html)|Data is persistent and durable. It grows and shrinks automatically as you add or remove files|Data is persistent and durable, with features like snapshots and automated backups[](https://dev.to/kouta222/aws-storage-services-comparison-s3-ebs-efs-and-fsx-4nm0)|
|**Access**|Attached to a single EC2 instance in a specific Availability Zone (AZ)[](https://dev.to/kouta222/aws-storage-services-comparison-s3-ebs-efs-and-fsx-4nm0)|Attached to a single EC2 instance as a raw, unformatted disk[](https://docs.aws.amazon.com/en_us/AWSEC2/latest/UserGuide/Storage.html)|Can be mounted on multiple EC2 instances across different AZs simultaneously[](https://awstip.com/unlocking-aws-ec2-storage-a-complete-guide-to-ebs-efs-instance-store-526e74e8e06d?gi=46bff44d1149&source=collection_home---4------1-----------------------)|Can be mounted on multiple instances (Linux & Windows) and even on-premises servers[](https://repost.aws/pt/articles/ARvjfcft0UT-6I1SBRoLDkCw/storage-differentiators)|
|**Use Cases**|Boot volumes, relational (e.g., MySQL) & NoSQL databases (e.g., MongoDB, Cassandra), data warehousing, ERP systems[](https://repost.aws/pt/articles/ARvjfcft0UT-6I1SBRoLDkCw/storage-differentiators)[](https://dev.to/1suleyman/how-i-started-building-secure-cloud-apps-on-aws-and-what-i-learned-about-iam-ec2-and-root-386a)|Temporary storage for caches, buffers, scratch data, and high-performance temporary storage[](https://dev.to/1suleyman/how-i-started-building-secure-cloud-apps-on-aws-and-what-i-learned-about-iam-ec2-and-root-386a)|Shared storage for web serving, content management, home directories, container storage, analytics[](https://repost.aws/pt/articles/ARvjfcft0UT-6I1SBRoLDkCw/storage-differentiators)[](https://dev.to/1suleyman/how-i-started-building-secure-cloud-apps-on-aws-and-what-i-learned-about-iam-ec2-and-root-386a)|**FSx for Lustre:** HPC, ML training, big data, media processing[](https://repost.aws/pt/articles/ARvjfcft0UT-6I1SBRoLDkCw/storage-differentiators)  <br>**FSx for Windows:** Windows file shares, SMB workloads, enterprise apps[](https://repost.aws/pt/articles/ARvjfcft0UT-6I1SBRoLDkCw/storage-differentiators)|
|**Key Advantage**|**Persistent, durable, and flexible**: Detachable, snapshot backups, independent instance lifecycle[](https://docs.aws.amazon.com/en_us/AWSEC2/latest/UserGuide/Storage.html)|**Ultra-low latency**: Direct NVMe connection with no network hop[](https://blog.devops.dev/understanding-latency-differences-between-aws-storage-services-a-practical-guide-4abf79470c0d)|**Shared & elastic**: Multiple instances can access the same data, auto-scaling storage[](https://dev.to/kouta222/aws-storage-services-comparison-s3-ebs-efs-and-fsx-4nm0)|**Specialized & fully-managed**: Enterprise-grade performance (HPC, Windows) without the management overhead[](https://dev.to/kouta222/aws-storage-services-comparison-s3-ebs-efs-and-fsx-4nm0)|
|**Key Limitation**|**Network latency**: Single-digit ms latency (though io2 Block Express is sub-ms).  <br>**AZ-bound**: Snapshots are needed to move across AZs[](https://awstip.com/unlocking-aws-ec2-storage-a-complete-guide-to-ebs-efs-instance-store-526e74e8e06d?gi=46bff44d1149&source=collection_home---4------1-----------------------)|**Ephemeral**: Data loss upon instance stop/termination[](https://docs.aws.amazon.com/en_us/AWSEC2/latest/UserGuide/Storage.html)|**Higher latency** than EBS/Instance Store due to network NFS overhead[](https://blog.devops.dev/understanding-latency-differences-between-aws-storage-services-a-practical-guide-4abf79470c0d)|**More expensive** and often overkill for simple shared storage needs|















# Storage Gateway

a hybrid cloud storage service that connects your existing on-premises environments with the AWS Cloud. Customers use Storage Gateway to simplify storage management and reduce costs for key hybrid cloud storage use cases. These include moving tape backups to the cloud, reducing on-premises storage with cloud-backed file shares, providing low latency access to data in AWS for on-premises applications, as well as various migration, archiving, processing, and disaster recovery use cases.

AWS Storage Gateway service provides three different types of gateways – Tape Gateway, File Gateway, and Volume Gateway – that seamlessly connect on-premises applications to cloud storage, caching data locally for low-latency access.

Gateway Storage Types Overview:


![[Storage-gateway-types.jpg]]

# Quiz


Question 1:

Which EC2 Storage would you use to create a shared network file system for your EC2 Instances?

EFS

Amazon EFS is a fully managed service that makes it easy to set up scale, and cost-optimize file storage in the amazon cloud

Question 2:
Which service can be used to automate image management processes?

EC2 Image builder


Question 3:

Which of the following is a fully managed native Microsoft Windows file system?

FSx


Question 4:

What are AMIs NOT used for?

Add your own IP addresses

You cannot use AMIs to add your IP addresses. IP addresses are added to an instance as you can create it

However you can:

Add your own software license

Add your own config

add your own OS

Question 5:

EBS Volumes CANNOT be attached to multiple EC2 instances at a time.

True

EBS volumes can only be attached to one EC2 instance at a time, but EC2 instances can have multiple EBS Volumes attached to them

True

EBS Volumes allows instances' data to persist even after their termination

Question 7:

Which statement is CORRECT regarding EC2 Instance Store?

It has better I/O performance, but the data is lost if the EC2 instance is terminated

Question 8:

What is an EBS Snapshot?

A backup of your EBS Volume at a point in time

EBS snapshots are used to backup data on your EBS Volumes at a point in time


Question 9:

Where can you find a third party's AMI so you can use it to launch your EC2 Instance?

AWS Marketplace AMIs

You can use AWS Marketplace AMIs to use someone else's AMI


Question 10:

What is an EBS Volume tied to?

An availability zone

EBS Volumes are tied to only one availability zone

because EBS volumes are specifically designed to be associated with one availability zone, which helps ensure low latency and high availability for your applications