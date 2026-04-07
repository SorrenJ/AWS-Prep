

# Docker

Platform to deploy app

package applications and their dependencies into standardized units called containers

Apps packaged in containers that can be run on any OS


Apps run the same, regardless where they are run

scale containers up and down quickly


## Containers

lightweight, portable, self-suffcient sofrtware package

It contains:

Application code

runtime (Node.js, Python, etc.)

System Libraires

config files

### Components of a container

#### Docker Image 
read-only template with instructions for creating a container

 Stored in Docker Repositories

### Docker Container

A running instance of an image, isolated, lightweight process on your machine

You can run multiple containers from the same image

### Dockerfile

Textfile with instruction to build an image



## Docker Vs. Virtual Machines


### Virtual Machine Arch

``` text
+-------------------------------------------------+
|                 App A      App B                |
|                 (MySQL)   (Nginx)               |
+-------------------------------------------------+
|             Guest Operating System              |
|                (Ubuntu 22.04)                   |
+-------------------------------------------------+
|                 Hypervisor                      |
|          (VMware, Hyper-V, VirtualBox)          |
+-------------------------------------------------+
|             Host Operating System               |
+-------------------------------------------------+
|                  Hardware                       |
+-------------------------------------------------+

```


1. Hypervisor creates virtual hardware (CPU, RAM, disk, network)
2. Each VM gets a full operating system (Windows, Linux, etc.)
3. Apps run on top of the guest OS
4.  **Result:** Heavy, slow, but strong isolation


###  Docker Arch

``` text
+-------------------------------------------------+
|     Container A     Container B     Container C |
|     (Node.js)       (Redis)         (PostgreSQL)|
+-------------------------------------------------+
|            Docker Engine / Container Runtime    |
+-------------------------------------------------+
|            Host Operating System                |
|            (Linux Kernel / Windows Kernel)      |
+-------------------------------------------------+
|                  Hardware                       |
+-------------------------------------------------+
```

1. Docker engine runs on host OS
2. Containers share the host's kernel
3. Each container gets isolated userspace (file processes, network)
4. Result: Lightweight, fast, efficient resource usage

# ECS

Elastic Container Service

a highly scalable, fast, container management service that makes it easy to run, stop, and manage Docker containers on a cluster. 

You cannot use Amazon Elastic Container Service (Amazon ECS) to store and deploy docker container images.


Launch Docker containers on AWS

Has EC2 instances servers that MUST BE MANAGED by you

But AWS takes care of the starting / stopping containers

Has integrations with the Application Load Balancer

![[Screenshot 2026-02-05 205524.png]]



# Fargate


Launch Docker container on AWS

NO NEED TO PROVISION NO MANAGE -> no EC2 instances

Serverless

![[Screenshot 2026-02-05 210109.png]]


# ECR

elastic container registry

can be used to store, manage, and deploy Docker container images. Amazon Elastic Container Registry (Amazon ECR) eliminates the need to operate your container repositories. You can then pull your docker images from Amazon Elastic Container Registry (Amazon ECR) and run those on Amazon Elastic Container Service (Amazon ECS).
![[ECR-diagram.png]]
storage for your docker images to be used and run by ECS or Fargate




![[Screenshot 2026-02-05 210856.png]]


# EKS


Elastic Kubernetes Service

launch managed Kubernetes cluster on AWS

![[Screenshot 2026-02-05 213208.png]]



# Serverless

developers don’t have to manage servers, it means you just don’t manage / provision / see them

Serverless services: Amazon S3, DynamoDB, Fargate, Lambda


# Lambda

No servers to manage

AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers. 

You upload your code (in languages like Python, Node.js, Java, etc.), and Lambda runs it only when triggered, charging you for every millisecond your code executes and the number of times it's triggered.

Runs code through functions


Example usage: Serverless Thumbnail creation![[Screenshot 2026-02-05 220504.png]]



Run a serverless cron job

Pay per calls , but first million requests are free

pay per duration (in increment of 1 ms)

usually very cheap -> so popular



## **Common Use Cases:**

- **Real-time file processing** (resize images when uploaded to S3)
    
- **Backends for mobile/web apps** via API Gateway
    
- **Scheduled tasks** (cron jobs)
    
- **Chatbots and voice assistants**
    
- **Data processing pipelines**
    
- **Automated backend tasks**


# API Gateway

Server less

Used for developer to easily create, publish, maintain apis


# Batch

Launch and run EC2 instances (batch jobs), dynamically

Batch jobs are defined as Docker images and run on ECS -> packaged as Docker containers and executed on Amazon ECS

You submit or schedule batch jobs and AWS Batch does the rest!

Helpful for cost optimizations and focusing less on the infrastructure![[Screenshot 2026-02-05 231629.png]]

They are NOT serverless

# Lightsail

Great for people with little cloud experience

Minimal Virtual servers, storage, databases, and networking

Use cases:
• Simple web applications (has templates for LAMP, Nginx, MEAN, Node.js…)
• Websites (templates for WordPress, Magento, Plesk, Joomla)
• Dev / Test environment


predictable & low pricing for simple application & DB stacks



# Quiz

Question 1:
How do you get charged in AWS Lambda?

Per call and per duration



Question 2:
You would like to launch Docker containers in AWS without worrying about provisioning or managing any infrastructure. The Docker containers will be used to host a heavy workloads to serve different types of requests. Some requests may need up to 30 minutes to be completed. Which AWS service should you use to run Docker containers in a Serverless way and satisfy the requirements?

Fargate

Fargate is the correct choice because it allows you to run Docker containers in a completely serverless environment, meaning you don’t need to manage any underlying infrastructure, which is crucial for hosting workloads that may take up to 30 minutes to complete. This aligns perfectly with your requirement to launch containers without worrying about provisioning and managing servers.


Question 3:
A complete cloud beginner would like to create a simple application with predictable pricing. What service should this person use?

Lightsail

Question 4:
What is the name of the software development platform that allows you to run applications the same way, regardless of where they are run?

Docker

Question 5:
How would you best describe "event-driven" in AWS Lambda?

Happens when needed

Functions are invoked when needed. They are triggered


Question 6:
Which AWS service allows you to launch Docker containers on AWS, but requires you to provision and maintain the infrastructure?

ECS

Question 7:
Which of the following statements is INCORRECT regarding the definition of the term "serverless"?

There are no server. You do not manage, provision and see them, but they do exist

Question 8:
Which of the following statements is NOT a feature of AWS Lambda?

Definition of a minimum and a maximum of EC2 instances running

This is a feature of Auto Scaling Groups, not AWS Lambda

Question 9:
A company needs to run thousands of jobs but would like to NOT manage the compute resources. What service can it use?

Batch

enables to easily run hundreds of thousands of batch computing jobs on AWS. Dynaimically provisions the optimal quantity and type of compute resources (i.e. CPU or memory optimized instances) based on volume and specific resources requirements of the batch jobs submitted


Question 10:
Where should you store your private Docker images so they can be run by ECS or Fargate?

Elastic Container Registry

a service where you store your Docker image so they can be run by ECS or Fargate


Question 11:
Which AWS serverless service can be used by developers to create APIs?

API Gateway

A fully managed serverless service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale