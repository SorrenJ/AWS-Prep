
# Organizations

allows to manage multiple aws accounts

with main account being the master account

consolidated billing - single payment for all accounts

pricing beneits

API avialable for account creation

Use service control policies (SCP)

AWS Organizations helps you to centrally manage billing; control access, compliance, and security; and share resources across your AWS accounts. Using AWS Organizations, you can automate account creation, create groups of accounts to reflect your business needs, and apply policies for these groups for governance. You can also simplify billing by setting up a single payment method for all of your AWS accounts. AWS Organizations is available to all AWS customers at no additional charge.



## Multi accounts

tagging standards for billing

enavle cloudtrail to send logs for all accounts

cloudwatch logs

## Root OU

contains everything , it contains master accounts

you can create differen t OUs like Dev OU, Prod OU

witiin Prod OU you can have Finance OU, HR OU, , etc..


## Service Control Policies (SCP) 


Whitelist or blacklist IAM actions, applied at the OU or account level, but doesn't apply to master account or service linked roles

must have an explicit allow (doesn't allow anything by default)

Use cases:

restrict access to certain services (i.e. can't use EMR) for example in in production account

Enforce PCI compliance by explicitly disabling services

![[Pasted image 20260316131720.png]]
Blacklisting

An SCP looks just like a IAM Policy. So this is Allow all actions. So we allow STAR on STAR. So do you say you can do anything but DenyDynamoDB. And we're saying the effect is Deny on DynamoDB Star for any resource.


![[Pasted image 20260316132012.png]]
White Listing
whitelist only a certain type of services. So we're saying allow EC2 star and CloudWatch star on Resource Star, but any other services but EC2 and CloudWatch, cannot be usable.


## Consolidated Billing

Share the volume pricing, reserved instances and saving plans discounts, 

get one bill for all AWS accounts in aws organization

which really can help your accounting departments and allow you not to be restricted in how many accounts you can create for AWS



![[Screenshot 2026-03-16 185922.png]]

So, let's take an example of

Reserved Instance Sharing.

So we have an organization with two accounts and in the first one, account A, there is no Reserved Instances, and account B, there are five reserved EC2 instances.

Now, let's assume that we are within one AZ because Reserve Instances are at the AZ level and we have nine EC2 instances.

As you can see, three are launched in account B, and six are launched in account A.

Now, what is going to happen?

Well, if we have five EC2 Reserved Instances on account B, then the three EC2 instances obviously are going to be reserved, but because we have enabled Reserved Instances sharing, then two instances in account A will also benefit from Reserved Instances pricing and therefore rebuking cost savings. So, at the end of the day, we have five Reserved Instances and four not Reserved Instances in this use case even though Susan in account B only launched three EC2 instances out of the five that were reserved.

## Control Tower

Easy way to set up and govern a secure and compliant multi-account AWS environment based on best practices

Benefits

automated setup for environments, policy management using guard rails

Control tower runs on top of AWS organizations and sets up the organizations to organize accounts and implement SCP

## Resource Access Management


Share  AWS resources with other AWS accounts that are owned by your account within your organization

i.e.  Aurora, VPC subnet, transit Gateway


## Service Catalog

a quick self-service portal to launch a set of authorized products, predefined by admins (i.e. virtual machines databases, storage options)

And products are just CloudFormation templates with the proper parameters.

And you can include them in a portfolio, and a portfolio is a collection of products.

And then you define who has access to launching what products within my portfolio. And then as a user, you log in to your portal on Service Catalog and you have a quick list of all the products that you can use because of your permissions. And then the users can launch these products and automatically they get provisioned by CloudFormation.


So say for example, that a user wants to have access to a quick RDS database but doesn't know how to create one properly. Then you could offer this as a service from within the Service Catalog.

# Pricing

with a new AWS account, you get up to $200 in credits


There are three fundamental drivers of cost with AWS: compute, storage, and outbound data transfer. In most cases, there is no charge for inbound data transfer or data transfer between other AWS services within the same region. Outbound data transfer is aggregated across services and then charged at the outbound data transfer rate.


## Pricing Models

### Pay as you go
pay for what you use, remain agile, responsive, meet scale
demands

### Save when you reserve
minimize risks, predictably manage budgets, comply with long-terms requirements

Reservations are available for EC2 Reserved Instances, DynamoDB Reserved Capacity, ElastiCache Reserved Nodes, RDS Reserved Instance, Redshift Reserved Nodes

### Pay less by using more:
volume-based discounts

### Pay less as AWS grows

## Free Plan

expires in 6 months or when credit are consumed (no charges)

## Paid Plan 



charged after you consume your credits

| Service                               | Pricing Model / Key Factors                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Additional Details / Examples           |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| **EC2 (Elastic Compute Cloud)**       | • Charged for what you use: number of instances, configuration (physical capacity, region, OS/software, instance type/size), ELB running time & data processed, detailed monitoring.  <br>• **On‑demand**: min 60s, per second (Linux/Windows) or per hour (other).  <br>• **Reserved**: up to 75% discount, 1 or 3 yr commitment, payment options (all upfront, partial, no upfront).  <br>• **Spot**: up to 90% discount, bid for unused capacity.  <br>• **Dedicated Host**: on‑demand or 1/3 yr reservation.  <br>• Savings Plans as alternative. |                                         |
| **Lambda**                            | • Pay per call (number of requests).  <br>• Pay per duration (compute time).                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |                                         |
| **ECS (EC2 Launch Type)**             | • No additional fees; you pay for the AWS resources your application creates and stores (e.g., EC2 instances, EBS volumes).                                                                                                                                                                                                                                                                                                                                                                                                                           | Underlying resources billed separately. |
| **Fargate (Launch Type)**             | • Pay for vCPU and memory resources allocated to your containers.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | No need to manage underlying EC2.       |
| **S3 (Simple Storage Service)**       | • Storage class (Standard, Infrequent Access, One-Zone IA, Intelligent Tiering, Glacier, Deep Archive).  <br>• Number and size of objects (tiered pricing by volume).  <br>• Number and type of requests.  <br>• Data transfer OUT of the S3 region.  <br>• S3 Transfer Acceleration.  <br>• Lifecycle transitions.  <br>• Similar service: EFS (pay per use, infrequent access & lifecycle rules).                                                                                                                                                   |                                         |
| **EBS (Elastic Block Store)**         | • Volume type (performance), storage volume in GB per month provisioned.  <br>• IOPS: General Purpose SSD (included), Provisioned IOPS SSD (provisioned amount), Magnetic (number of requests).  <br>• Snapshots: added data cost per GB per month.  <br>• Data transfer: outbound tiered volume discounts, inbound free.                                                                                                                                                                                                                             |                                         |
| **RDS (Relational Database Service)** | • Per hour billing.  <br>• Database characteristics: engine, size, memory class.  <br>• Purchase type: On‑demand, Reserved (1/3 yr, optional upfront).  <br>• Backup storage: no additional charge up to 100% of total database storage per region.  <br>• Additional storage per GB per month.  <br>• Number of I/O requests per month.  <br>• Deployment type: Single AZ, Multi‑AZ (storage and I/O variable).  <br>• Data transfer: outbound tiered volume discounts, inbound free.                                                                |                                         |
| **CloudFront (CDN)**                  | • Pricing varies across geographic regions (aggregated per edge location).  <br>• Data Transfer Out (volume discount).  <br>• Number of HTTP/HTTPS requests.                                                                                                                                                                                                                                                                                                                                                                                          |                                         |



Use Private IP instead of Public IP for good savings and better network performance

Use same AZ (1 zone) for maximum savings (sacrifice  high availability)


## Savings Plan

Commit a certain $ amount per hour for 1 or 3 yrs, easiest way to setup long-term commitments on AWS


### EC2 Savings plan


commit to usage to individual instances families in a REGION, 

upto 72% discount compared to On-Demand

regardless of size, tenancy, and OS


### Compute Savings Plan

For Ec2 instance usage, fargate, lambda SERVICE USAGE

regardless of region, instance family size, tenancy, OS

save up to 66%

### SageMaker Savings Plans (ML Savings Plan)

For SageMaker service  usage

regardless of region, instance family, and component

[Compute Savings Plans](https://aws.amazon.com/savingsplans/compute-pricing/)


## Compute Optimizer

contains the most comprehensive set of AWS cost and usage data available, including additional metadata about AWS services, pricing, and reservations


So it's going to do an analysis of your EC2 instances, your auto scaling groups,
and tell you, for example, which one are over-provisioned or under provisioned and then you can build your optimizations and then you can have a better cost perspective and also a better performance.



AWS Compute Optimizer helps you identify the optimal AWS resource configurations, such as: 

- Amazon EC2 instance types, 

- Amazon EBS volume configurations, and 

- AWS Lambda function memory sizes, 

using machine learning to analyze historical utilization metrics.

AWS Compute Optimizer delivers recommendations for selected

- types of EC2 instances, 

- EC2 Auto Scaling groups, 

- Amazon EBS volumes, and

- AWS Lambda functions.


## Billing and costing Tools

### Pricing calculator
estimate costs for your cloud architectre the cloud

[AWS Pricing Calculator](https://calculator.aws/#/)

can get very grannular

![[Pasted image 20260317182628.png]]

## Tracking costs in the cloud
### Billing Dashboard

This is a very high level tool,

but it will be helpful

to just get an overview of what's happening

### Cost allocation tags

track your AWS costs on a detailed level

you export an excel report 

Tags: used for organizing resources like  EC2 instances, load balances, RDS, VPC resources, etc. Can be used to create resource groups for cost allocation tags


uses user generated tags, or aws generated tags , will be automatically applied to the resource that you created

![[Pasted image 20260317184844.png]]


### Cost and Usage Reports

You can generate a cost and user report, the most granular report

So you can get some information, for example, around your Amazon EC2 Reserved Instances usage. This cost report will give you all the usage for each service category used by an account and its IAM users in hourly or daily line items, as well as any tags that you have activated for cost allocation purposes.

![[Pasted image 20260317185821.png]]



### Cost Explorer

Analyze your data at a high level: total costs and usage across all accounts, Or Monthly, hourly, resource level granularity

AWS Cost Explorer has an easy-to-use interface that lets you visualize, understand, and manage your AWS costs and usage over time. AWS Cost Explorer includes a default report that helps you visualize the costs and usage associated with your top five cost-accruing AWS services, and gives you a detailed breakdown of all services in the table view.

Create custom reports that analyze cost and usage data.

Forecast usage up to 12 months based on previous usage

The rightsizing recommendations feature in AWS Cost Explorer helps you identify cost-saving opportunities by downsizing or terminating Amazon EC2 instances. You can see all of your underutilized Amazon EC2 instances across member accounts in a single view to immediately identify how much you can save.

![[Pasted image 20260317190609.png]]



### Billing Alarms

It’s for actual cost, not for projected costs

Intended a simple alarm (not as powerful as AWS Budgets)
###  Budgets

Create budget and send alarms when costs exceeds the budgets

Types of budgets:

- Usage
- Cost
- Reservation
- Savings Plans

AWS Budgets cannot be used to identify under-utilized EC2 instances without manually configuring coverage targets
### Cost Anomaly Detection

Continuously monitor your cost and usage using ML to detect unusual spends

And you don't have to define anything, you don't have to define thresholds. It just knows on its own what looks a little bit weird.

![[Screenshot 2026-03-18 130144.png]]


### Service Quotas

Notifies you when you are close to a service quota value threshold, Create CloudWatch Alarms, on the Service Quotas console

example: Lambda concurrent executions

and you can request quota increase directly from the consult.

##  Trusted Advisor

Anaylze your AWS accounts and provides reccomendation on 6 categories

gives you a high level account assessment on your account. It's going to check for a few things and advise you on them.

1. Cost optimization
2. Performance
3. Security
4. Fault tolerance
5. Service limits
6. Operational Exellence


## Support Plans Pricing

### Basic Support Plan : Tier 1

FREE 

customer service & communities

AWS trusted advisior

Personal health dashboard



### Developer Support Plan: Tier 2

Has all of Basic support plan plus more stuff

Business hours and email access to cloud support associates

unlimited cases, unlimited contacts


### Business Support Plan: Tier 3

To be used for production workloads

THE most Cost-effective option that offer 24x phone, email, and chat support

Has Trusted Advisor for full set of checks and api access

access to infrastucture event management for additional fee

unlimited cases, unlimited contacts


### Enterprise On-Ramp Support Plan: Tier 4

For production or business critical workloads

Has all of Business Support Plan plus more stuff


Access to Technical Account Manager (TAM)

**APN Technology Partner** - APN Technology Partners provide hardware, connectivity services, or software solutions that are either hosted on or integrated with, the AWS Cloud. APN Technology Partners cannot help in migrating to AWS and managing applications on AWS Cloud.

Conceirge support Plan

Concierge Support Team - The Concierge Support Team are AWS billing and account experts that specialize in working with enterprise accounts. They will quickly and efficiently assist you with your billing and account inquiries. The Concierge Support Team is only available for the Enterprise Support plan. Concierge Support Team cannot help in migrating to AWS and managing applications on AWS Cloud.


Reviews 

Business critical system downtime less than 30 minutes
### Enterprise Support Plan: Tier 5

For mission critical workloads

Has all of Business Support Plan plus more stuff

DESIGNATED access to Technical Account Manager (TAM)

Incident detection and response for an additional fee

Business critical system downtime less than 15 minutes


# Quiz: Account Management, Billing & Support

Question 1:

Which of the following allows you to centrally manage all users and roles permissions in your AWS Organization?

Service Control Policies (SCP)

Service control policies (SCPs) are a type of organization policy that you can use to manage permissions in your organization. An SCP spams all IAM users,  groups, and roles, including the AWS account root user

Question 2:

You would like to automatically set up and govern a secure multi-account AWS environment with best practices for your organization. Which AWS tool can you use?

Control Tower

Control tower offers the easiest wat to set up and govern a new, secure, ,multi-account AWS environment. It establishes a landing zone that is based on best-practices blueprints, and enables governance using guardrails you can choose from a pre-packaged list

Question 3:

A company would like recommendations regarding its performance, security, and fault tolerance. What can it use?

Trusted Advisor

AWS Trusted Advisor is an online tool that provides you real time guidance to help you provision user resources following AWS best practices, including performance, security, and fault tolerance, but also cost optimization and service limits

Question 4:
Which of the following is INCORRECT regarding AWS Organizations?

Faster access to the AWS support

AWS Organization does not offer faster access to the AWS Support

It DOES:

Manage multiple AWS accounts

Consolifated billinf across all accounts

Volume discounts from aggregated usage


Question 5:
What is the most cost-effective option to have 24x7 phone, email, and chat support?


Business Support Plan

The most cost effective option that offers 24x7 phone, email, and chat support

Question 6:

What can you use to estimate the cost of your architecture solution?

Simple Monthly Calculator/Pricing Calculator

an esy to use online toll that enables you to estimate their architecture solution monthly coist of AWS services for your use case based on your expected usage, It is being relpaced by AWS Pricing Calculator


Question 7:

The Enterprise Support Plan comes with a business-critical system down response under 15 minutes and offers access to a Technical Account Manager, as well as a Concierge Support Team.

The enterprise support plan come with a business-critical system down reponse under 15 minutes and offers access to a technical account manager, as well as a concierge support team. it is the only plan to have these features



Question 8:

A company is not sure whether or not it is cost-effective to migrate to the AWS Cloud. Which service can help the executive board make a decision?

Pricing Calculator

A web based service that you can create cost estimates to suit your AWS use cases. AWS Pricing Calculator is useful both for people who have never used AWS and for those who want to reorganize or expand their usage


Question 9:
What do Resource Groups rely on to group your resources?

Tags

u can assign metadata to your AWS resources in the form of tags. tags can help you  manage, identify, organize, search for, and filter resources

Question 10:
What can you use to get alerts when your costs and usage are exceeding or are forecasted to exceed your budgeting amount?

Budgets 

gives you the ability to set custom budgets that alert you when your costs or usage exceed (or are forecasted to exceed) your budgeted amount. Difference with your CloudWatch Billing Alarms: CloudWatch Billing Alarms only send alerts when your costs and usage are exceeding your budget, not when it is forecasted to exceed your budget, while AWS budget does both 

AWS Budgets can analyze your current usage and spending patterns to forecast whether your costs are likely to exceed your budget, enabling you to act before the overage actually happens. This proactive feature makes Budgets more suitable for managing costs and usage based on forecasts rather than only reactive monitoring of already incurred charges.

Question 11:
A company would like to choose the best Savings Plan and forecast its cost in the next 3 months. Which AWS service can help?

Cost Explorer

Can be used to forecast usage up to 12 months based on the previous usage. It can also be used to choose optimal Savings Plan. Cost Expolorer has an easy-to-use interfafe that let's you visualize, understand, and manage your aws costs and usage overtime

Question 12:
Which of the following options uses machine learning to recommend optimal AWS resources and therefore reduces costs?

Compute Optimizer

recommends optimal AWS resources for your workloads to reduce costs and improve performance by using machine learning to analyze historical utilization metrics




# Quiz: Pricing


Question 1:

Which services are free to use in AWS?


IAM, VPC, Consolidated Billing, and Elastic  Deanstalk

IAM (Identity and Access Management), VPC (Virtual Private Cloud), and Consolidated Billing do not incur costs when used, while Elastic Beanstalk itself is also free, but it's crucial to note that the resources you create within it may have associated costs. This understanding emphasizes the importance of differentiating between service usage and the resources related to those services.



Correct answer. Good job!

Question 2:

CloudFront pricing is the same in every geographic region.

FALSE

CloudFront pricing varies by geographic region, reflecting the different costs associated with servers and infrastructure in those locations. This highlights the importance of understanding how pricing can differ based on where services are utilized.



Correct answer. Good job!
Question 3:
When you reserve, the larger the upfront payment, the smaller the discount.


False, the larger the upfront, the bigger the discount

You selected "False, the larger the upfront, the bigger the discount" because a higher upfront payment typically provides better discounts on reserved instances, making them more cost-effective in the long run. This concept is crucial for understanding how to optimize costs when utilizing cloud services.


Question 4:
Which of the following is NOT a pricing factor in S3?

Data transfer into S3

The following pricing factors are
- storage class
- Object size
- Type of requests



You selected "Data transfer into S3" as your answer, which is correct because inbound data transfers to S3 are free of charge. Understanding this pricing aspect is essential as it helps you manage your storage costs effectively while utilizing S3.


Question 5:
EBS Snapshots are added cost in GB per month.

Correct answer. Good job!
Question 5:
EBS Snapshots are added cost in GB per month.

TRUE 

Your answer is correct because EBS Snapshots incur an additional cost based on the GB of data stored per month, which impacts your overall EBS pricing. Understanding this helps you budget effectively for storage costs in AWS.

Was this content relevant to you?


Question 6:

Which of the following options can provide up to 66% discount compared to On-demand for a commitment to a consistent amount of usage for 1 or 3 years and offers the possibility to change EC2 instances family type?


Computer Savings Plans

You selected "Compute Savings Plans" because they offer flexibility and significant cost savings, helping you reduce your expenses by up to 66% when committing to a consistent amount of usage for 1 or 3 years.


Question 7:
You are running an on-demand Linux EC2 instance, what timing is applied regarding billing?


Pay per second

With Linux EC2 instances, you pay per second of compute capacity, there is also a minimum of 60s of use

You selected "Pay per second," which is correct because Linux EC2 instances charge by the second of usage, with a minimum billing of 60 seconds. This understanding is crucial in managing your costs effectively when running instances in AWS.


Question 8:

Which pricing model allows you to minimize risks, predictably manage budgets, and comply with long-term requirements, and is available for EC2, DynamoDB, ElastiCache, RDS, and Redshift?


NOT Pay as you go

is a model where you pay for what you use, remain agile, repsonisve, meet scale demands, no best suited for predicatble managing budgets and complying with long-term requirements

Save when you reserve
 
 because this pricing model allows you to make long-term commitments that minimize financial risks and ensure predictable budgeting, particularly for services like EC2 and RDS. Understanding this helps you effectively plan costs and align with your organization's usage needs.


Question 9:
Which RDS pricing option is the most cost-effective if you need capacity for 3 years?

Reserved Instances because this pricing option offers significant savings—up to 69% compared to On-demand pricing—by committing to a longer-term usage for your RDS instances, ideally suited for your capacity needs over 3 years. 