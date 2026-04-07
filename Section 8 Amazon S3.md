## Intro

One of the main building blocks of AWS

Use Cases: Backup and storage, Disaster Recovery, Archive, Hybrid Cloud Storage, Application hosting, Media Hosting, Data lakes & big data analytics, software delivery, static website

## Buckets

Allows people to store objects (files) in buckets (directories)

Buckets must have globally unique name

Buckets are defined and created at the region level (not a global service) -> buckets must be defined in a specific AWS region

Naming convention: no uppercase no underscore

## Objects

Objects are files in a bucket. Each of them contains a Key

s3://my-bucket/my_file.txt
s3://my-bucket/my_folder1/another_folder/my_file.txt

Key is composed of prefix (my_folder1/another_folder/) + object name (my_file.txt)

``` bash
s3://my-bucket/my_folder1/another_folder/my_file.txt
```

Slashes don't mean directories they are just for long names

Object values are the content of the body , max it can hold is 5TB

+5GB must use multi-part upload

Object can have meta data (their list of key and value pairs, and that could be set by the system or set by the user to indicate some elements about the file)

Objects can have tags (Unicode key / value pair – up to 10) – useful for security / lifecycle

Version ID


## Security


User-based
IAM Policies -> which API calls should be allowed for a specific user from IAM

Resource-Based
S3 introduces Resourse-based security

- Bucket Policies
- Object Access Control List
- Bucket Access Control List

### Bucket Policies

Bucket policies - You can assign bucket wide rules though the S3 console, allows a specific user or allow a user from another account -> this is called cross-account 

JSON based policies

- Resources tells the policy what buckets and object this policy applies on. The example shows it applies to every object `*`
- Effect chooses to Allow or Deny actions, we can either set for the APIs . In the example we Allo the action for GetObject
- Principal allows the account or user to apply the policy to. In this example  the `*` means the public reads on all objects inside the bucket

![[Pasted image 20251126223014.png]]



There are bucket settings for Block Public Access to prevent data leaks and if the Bucket should never be public

## Static Website Hosting


Can host static websites

```

The website URL will be (depending on the region)
• http://bucket-name.s3-website-aws-region.amazonaws.com
OR
• http://bucket-name.s3-website.aws-region.amazonaws.com

```

If you get a 403 Forbidden error, make sure the bucket
policy allows public reads!


## Versioning

Objects has version IDs
Best practice to version
 - Protect against unintended deletes (ability to restore a version)
- Easy roll back to previous version

## Replication 

S3 Replication is a feature that automatically and asynchronously copies objects across S3 buckets in the same or different AWS regions.

Replication types

Cross-Region Replication (CRR)

 - Replicates objects between buckets in different AWS regions
 - Usage: reduce latency for users in different regions

Same Region Replication (SRR)

- Replicates objects between buckets in the same AWS region
-  Usage: Aggerating logs from multiple buckets

Buckets can be in different AWS accounts

Copying is asynchronous

Must give proper IAM permissions to S3


## Durability and Availability


High durability (99.999999999%, 11 9’s) of objects across multiple AZ, Same for all storage classes

Availability Measures how readily available a service is, Varies depending on storage class


# Storage Classes



![[pt2-q16-i1.jpg]]






## General Purpose

Used for frequently accessed data

## Infrequent Access

Used for less frequently accessed data, i.e.. disaster recovery, backups

One Zone infrequent Access

Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA) is for data that is accessed less frequently but requires rapid access when needed. Unlike other S3 Storage Classes which store data in a minimum of three Availability Zones (AZs), Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA) stores data in a single Availability Zone (AZ) and costs 20% less than Amazon S3 Standard-Infrequent Access (S3 Standard-IA). Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA) offers the same high durability, high throughput, and low latency of S3 Standard, with a low per GB storage price and per GB retrieval fee. Although Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA) offers less availability than S3 Standard but that's not an issue for the given use-case since the thumbnails can be regenerated easily.

As the thumbnails are rarely used but need to be rapidly accessed when required, so Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA) is the best choice for this use-case.

## Glacier Storage 

Low cost object storage meant for archiving / backup


## Intelligent - Tiering

small monthly monitoring and auto-tiering fee

moves objects automatically btwn Access Tiers based on usage

has different tiers for frequency


# Express One Zone

High performance, single Availability Zone storage class
Objects stored in a Directory Bucket (bucket in a single AZ)

use cases: latency sensitive apps, data-intensive apps, AI & ML training, financial modeling

# Encryption

## Server - Side encryption 

Default

Server encrypts the file after recieving it
## Client-Side Encryption

User encrypts the file before uploading it

# IAM Access Analyzer for S3

This is a monitoring feature that ensures that only intended people have access to your S3 buckets

allows you to find out resources in your account that are shared with other entities


# Shared responsibilities for S3

AWS is responsible for

- Infrastructure
-  Configuration and vulnerability analysis
- Compliance validation

You are responsible for

- S3 versioning
- S3 Bucket Policies
- S3 Replication setup
- Logging and Monitoring
- S3 Storage Classes
- Data encryption at rest and in transit

# Snowball

Import data onto S3 through a physical device, edge computing

# Storage Gateway

Hybrid solution to extend on-premises storage to S3



# Quiz


Question 1:

Which S3 Storage Class is the most cost-effective for archiving data with no retrieval time requirement?

Amazon Glacier Deep Archive
Amazon Glacier Deep Archive is the most cost-effective option if you want to archive data and do not have a retrieval time requirement. You can retrieve data in 12 or 48 hours.


Question 2:

What hybrid AWS service is used to allow on-premises servers to seamlessly use the AWS Cloud at the storage layer?


AWS Storage Gateway is a hybrid cloud storage service that gives you on-premises access to virtually unlimited cloud storage.

Question 3:

What are Objects NOT composed of?

Access Keys are used to sign programmatic requests to the AWS CLI or AWS API.

Question 4:

Where are objects stored in Amazon S3?

Buckets store objects in Amazon S3.


Question 5:

What can you use to define actions to move S3 objects between different storage classes?

Lifecycle Rules can be used to define when S3 objects should be transitioned to another storage class or when objects should be deleted after some time.


Question 6:

A non-profit organization needs to regularly transfer petabytes of data to the cloud and to have access to local computing capacity. Which service can help with this task?

Snowball Edge Storage Optimized devices are well suited for large-scale data migrations and recurring transfer workflows, as well as local computing with higher capacity needs.

Question 7:

Which S3 Storage Class is suitable for less frequently accessed data, but with rapid access when needed, while keeping a high durability and allowing an Availability Zone failure?

Amazon S3 Standard-Infrequent Access allow you to store infrequently accessed data, with rapid access when needed, has a high durability, and is stored in several Availability Zones to avoid data loss in case of a disaster. It can be used to store data for disaster recovery, backups, etc.