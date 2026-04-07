
## Database types

Relational Databases

NoSQL Databases 
-> non relational 
-> purpose built for specific data models and have flexible schema for building modern application
Benefits
- Flexible
- scalability
- High perfromance for specific data model
- highly functional types optimized for data model

Example: key-value, document, graph, in memory, search databases

-> JSON 
- data can be nested
- Fields can change overime
- support for new typess: array

## Shared responsibility


Benefits include:
• Quick Provisioning, High Availability, Vertical and Horizontal Scaling
• Automated Backup & Restore, Operations, Upgrades
• Operating System Patching is handled by AWS
• Monitoring, alerting


Amazon S3 Standard-Infrequent Access allow you to store infrequently accessed data, with rapid access when needed, has a high durability, and is stored in several Availability Zones to avoid data loss in case of a disaster. It can be used to store data for disaster recovery, backups, etc.


## Amazon RDS

RDS stands for Relational Database Service
It’s a managed DB service for DB use SQL as a query language

Advantage over using EC2

RDS is a managed service
-> auto provisioning, OS patching
-> backups, and restore to specific timestamp
-> dashboards
-> multi AZ setup for DR (Disaster Recovery)

cons cant ssh into instance

Easy to set up, operate, and scale a relational database in the cloud, suited for Online Transaction Processing (OLTP)

### RDS Solution Architecture

1.  Elastic load Balancer 
2.  EC2 instances -> Auto Scaling Group
3. Stored in SQL  Amazon RDS RDS db 

# Amazon Aurora

Aurora is a proprietary technology from AWS (not open sourced)

PostgreSQL and MySQL

5x performance improvement over MySQL on RDS

over 3x the performance of Postgres on RDS

Aurora storage automatically grows in increments of 10GB

Costs more


### Amazon Aurora Serverless

Automated database instantiation and Client auto-scaling based on actual usage

PostgreSQL and MySQL supported

No capacity planning needed, alot more cost effectiv than provisioning an Aurora cluster yourself
Use case: infrequent, intemittent or unpredicatable workloads

# RDS Deployments

RDS Multi-AZ deployments' main purpose is high avilability, and RDS Read replicas' main purpose is scalability. Moreover, Multi-Region deployments' main purpose is disater recovery and local performance

## Read Replicas (Read Scalability & Performance)

To scale out **read-heavy** database workloads. It's an **asynchronous** replication solution.

How it Works:

You create one or more (up to 15) read-only copies of your primary DB instance.

These replicas can be in the same AZ, a different AZ, or even a different AWS Region.


Key Benefits:

Offload Read Traffic: Direct reporting, analytics, or heavy read queries to the replicas, freeing up the primary for write transactions.

Disaster Recovery (DR) in another Region: A Read Replica in a different region can be promoted to a standalone instance to become a new primary in case of a regional outage.

## Multi-AZ (High Availability & Data Durability)

**Failover** for increased **availability** and **data durability**. It's a **synchronous** replication solution.

How it Works:

You have a primary DB instance in one Availability Zone (AZ).

AWS automatically provisions and maintains a standby replica of the primary instance in a different AZ within the same region.

Key Benefit:

Automatic Failover: In the event of a planned event (like OS patching, DB instance scaling) or an unplanned outage (AZ failure, instance failure, storage failure), RDS will automatically switch ("failover") to the standby replica. This process typically completes within 60-120 seconds.

No Application Changes Needed: Your application connects to a single DNS endpoint. During a failover, RDS automatically updates this endpoint's DNS record to point to the new primary, so your application connection string remains the same.


## Multi - Region

Disaster recovery in case of region issue

replication cost


![[rds-deployments-comparisons.jpg]]


# Amazon ElastiCache

a fully managed **in-memory caching** service that simplifies deployment and operation of open-source compatible in-memory data stores


# DynamoDB

serverless NoSQL database service.

Fast and flexible non-realtional databsase service for any scale

it can scale with no downtime

it can process millions of requests per second

fast and consistent in performance

fully managed

No servers to provision, patch, or manage, Automatic scaling based on traffic, Built-in high availability with multi-AZ replication


high performance at any scale




## Data type

a key-value and document database

![[Pasted image 20260130124423.png]]



## DynamoDB Accelerator (DAX)

Fully Managed in-memory cache for DynamoDB

this is going to give you a 10x performance improvement.

**Comparison:**

DAX is ONLY used for and is integrated with DynamoDB, while

ElastiCache can be used for other databases applications Amazon


## Global Tables


What Are Global Tables?
Multi-region, multi-active replication for DynamoDB tables. Think of it as having the same table simultaneously active in multiple AWS regions, with automatic bidirectional synchronization.

Core Concept


```text
US-East-1 Table    ↔  Replicates ↔    EU-West-1 Table
       ↑                                 ↑
  App in Virginia                   App in Frankfurt
```


Write to either region → data automatically replicates to all other regions

No primary/secondary - every region is active for both reads and writes

Typical replication latency: < 1 second

Key Benefits

1. Global Low-Latency Access

``` yaml
User in Tokyo:      → Reads/Writes to ap-northeast-1 (10ms latency)
User in London:     → Reads/Writes to eu-west-2 (20ms latency)
User in California: → Reads/Writes to us-west-2 (15ms latency)
```

2. Disaster Recovery & Business Continuity
	- **Automatic failover**: If one region goes down, route traffic to another
    
	- **Zero RPO/RTO** for regional outages (no data loss, immediate failover)


3. Data Locality Compliance
	- Keep customer data in their home region for GDPR/regulatory requirements
    
	- Global applications with local data storage



# Redshift

AWS Redshift is a fully managed, petabyte-scale cloud data warehouse service designed for fast, analytical querying of large datasets using SQL. It's optimized for OLAP (Online Analytical Processing) workloads rather than transactional processing (OLTP).

it’s not used for OLTP

• Load data once every hour, not every second
• 10x better performance than other data warehouses, scale to PBs of data


## AWS RedShift Serverless

an auto-scaling, on-demand version of Amazon Redshift that automatically provisions and scales data warehouse capacity based on your workload needs. You don't manage any infrastructure—just load and query your data


Run analytics workloads without managing data warehouse infrastructure

Pay only for what you use (save costs)

 Use cases: Reporting, dashboarding applications, real-time analytics…

# EMR

EMR stands for “Elastic MapReduce”

EMR helps creating Hadoop clusters (Big Data) to analyze and process
vast amount of data

The clusters can be made of hundreds of EC2 instances
EMR takes care of all the provisioning and configuration

Use cases: data processing, machine learning, web indexing, big data…
Hadoop Clusters


# Amazon Athena

serverless query service to analyze data stored in Amazon S3

uses standard SQL language to query the files, supports CSV, JSON, ORC, Avro 

data scanned costs $5 per TB

# Amazon QuickSight

Serverless machine learning-powered service the creates dashboards

Usages: 

business analystics

building visualizations


Integrated with RDS, Aurora, Athena, Redshift, S3

# DocumentDB


AWS implementation of MongoDB (NoSQL database)

Used to store, query, and index JSON data



# Amazon Neptune


fully managed graph database, works well with applications that work with highly connected datasets

Usages: Knowledge graphs (Wikipedia), fraud detection, recommendation engine, social networking

High available with replications across multiple AZs


# Amazon Timestream

fully managed, fast, scalable, serverless time series database

A serverless time series database is a specialized database system designed to store, process, and analyze timestamped data (time series data) without requiring you to manage infrastructure, servers, or capacity planning.


Common Use Cases:
IoT & Sensor Data - Device telemetry, environmental monitoring

Application Monitoring - Metrics, logs, performance data

Financial Data - Stock prices, transaction records

Industrial IoT - Equipment sensor data, predictive maintenance

Observability - Application and infrastructure monitoring


1000s times faster & 1/10th the cost of relational databases

Built-in time series analytics functions (helps you identify patterns in your data in near
real-time)


# Amazon Managed Blockchain


Blockchain -> u can build applications where multiple parties can execute transations without the need for a trusted, central authority


# AWS Glue

a service to manage extract, transform, and load (ETL) data

Usage cleaning, transforming data for analytics, sed by Athena, Redshift, EMR

Fully Serverless 

Uses a central repository to store structural and operational metadata for data assets caleed Glue Data Catalog



# Quiz

Which AWS database is a data warehouse?

Redshift

Question 3:
Which AWS service is always serverless and has SQL capabilities?

Athena


Question 4:

You would like to use a serverless service to prepare data so it can be loaded for analytics. Which service would you use?

Glue

Question 5:
Which relational database is a proprietary technology from AWS and is cloud-optimized?

Aurora

Question 6:
You would like to migrate databases to AWS while still being able to use the database during the migration. What service allows you to do this?

Database Migration Service (DMS)

Question 7:
How can you create Hadoop clusters to analyze and process a vast amount of data?

EMR

Question 8:
Which in-memory AWS database can you use to reduce the load off databases and has high performance, low latency?

Elasticache

Question 9:
What is the name of a central repository to store structural and operational metadata for data assets in AWS Glue?

Glue Data Catalog

Question 10:
Which of the following databases is a managed service with SQL capability suited for Online Transaction Processing (OLTP)?

RDS

Question 11:
You would like to set up a NoSQL database that can scale with no downtime and can handle millions of requests per second. Which AWS database is best suited for this work?

DynamoDB

Question 12:

Which AWS service can create complex graphs for fraud detection?

Neptune

Question 13:
Which AWS serverless service can use machine learning-powered business intelligence to create interactive dashboards such as business analytics?

QuickSight

Question 14:
A company would like to set up a fully managed MongoDB database. Which AWS database is best-suited for this task?

DocumentBD

Question 15:
Which exclusive DynamoDB feature is an in-memory cache that can improve your performance up to 10x?

DynamoDB Accelerator

Question 16:
RDS Multi-AZ deployments’ main purpose is high availability, while RDS Read replicas’ main purpose is scalability.

True

