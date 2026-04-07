
# CloudFormation


CloudFormation is going to be used when we have infrastructure as code, when we need to repeat an architecture in different environments, different regions, or even different AWS accounts.

 allows you to use programming languages or a simple text file to model and provision, in an automated and secure manner, all the resources needed for your applications across all Regions and accounts

A declarative way of outlining your AWS infrastructure, for any resources

Lets you model, provision, and manage AWS resources using templates

templates are JSON or YAML files

## Benefits

Infrastucture as code
• No resources are manually created, which is excellent for control
• Changes to the infrastructure are reviewed through code


Cost
• Each resources within the stack is tagged with an identifier so you can easily see how much a stack costs you
• You can estimate the costs of your resources using the CloudFormation template
• Savings strategy: In Dev, you could automation deletion of templates at 5 PM and
recreated at 8 AM, safely


Productivity
• Ability to destroy and re-create an infrastructure on the cloud on the fly
• Automated generation of Diagram for your templates!
• Declarative programming (no need to figure out ordering and orchestration)

Don’t re-invent the wheel
• Leverage existing templates on the web!
• Leverage the documentation

 Supports (almost) all AWS resources:
• Everything we’ll see in this course is supported
• You can use “custom resources” for resources that are not supported

![[Screenshot 2026-02-07 232813.png]]

Deploying EC2 with security groups






![[Screenshot 2026-02-07 233427.png]]
view your changes in your infrastructure 


![[Screenshot 2026-02-07 233137.png]]

Viewing your infrastructure template in application composer

# Cloud Development Kit (CDK)

Define your cloud infrastucture with a language i.e. Java, .Net, javaScript, Python

For example, you do not want to use CloudFormation directly because this is a YAML format.

code will be compiled into a CloudFormation template (JSON or YAML)

You can deploy infrastucture and application runtime code together



![[Pasted image 20260207233855.png]]

# Elastic Beanstalk

A developer centric view of deploying an app on AWS

It uses all components (EC2, ASG, ELB, RDS) -> all in one view

Platform as a service (PaaS)  **that allows you to deploy and scale web applications and services**

Free but you pay for the underlying instances

Managed service, You just manage the application code
single instance deployment

Supports many languages and envrionemnts

Health montioring




![[Screenshot 2026-02-08 005647.png]]


Creating a new environment with elastic beanstalk

# CodeDeploy

automates code deployments to any instance, including Amazon EC2 instances and instances running on-premises.

 makes it easier for you to rapidly release new features, helps you avoid downtime during deployment, and handles the complexity of updating your applications.

deploy & upgrade any application onto servers

deploys application automatically

works with EC2 and On-premises servers -> hybrid service

servers and instance must be provisioned ahead of time


# CodeCommit

Code needs to be stored before pushing to servers

it's like the AWS GitHub

CodeCommit source control service that hosts Git-based repos, collab with others, code changes are versioned

Fully managed, scalable, highly available, private secured, Integrated with AWS


# CodeBuild

Building service -> compiles source code, run tests, produces packages that are ready to be deployed

fully managed, serverless, secure, paya as you go pricing olny pay for the build time

# CodePipeline
Orchestrate the different steps to have the code automatically pushed to production

For CICD

From Code to Build To Deploy
# CodeArtifacts

Artifact management system -> storing and retrieving dependencies

Stores software packages


# Systems Manager (SSM)

Helps manage your EC2 and On-Premises systems scale -> hybrid service

 a fully-managed service that provides you with an interactive browser-based shell and CLI experience. It helps provide secure and auditable instance management without the need to open inbound ports, maintain bastion hosts, and manage SSH keys. AWS Systems Manager Session Manager helps to enable compliance with corporate policies that require controlled access to instances, increase security and auditability of access to the instances while providing simplicity and cross-platform instance access to end-users.

patching automation

run commands acorss entire fleet of servers

store parameter configuration with SSM parameter store


But first we install SSM agents onto the systems we control


![[Pasted image 20260209131702.png]]

AWS Systems Manager allows you to centralize operational data from multiple AWS services and automate tasks across your AWS resources. You can create logical groups of resources such as applications, different layers of an application stack, or production versus development environments.

With AWS Systems Manager, you can select a resource group and view its recent API activity, resource configuration changes, related notifications, operational alerts, software inventory, and patch compliance status. You can also take action on each resource group depending on your operational needs. AWS Systems Manager provides a central place to view and manage your AWS resources, so you can have complete visibility and control over your operations.

How AWS Systems Manager works:


![[pt5-q58-i1.jpg]]
## Session Manager


Allows you to start a secure shell on EC2 or on-premise server

No SSH access, No SSH keys needed

### Parameter Store

Secures storage for config and secrets -> API Keys, passwords

Control acess permissions using IAM

Version tracking




# Quiz

Question 1:

Which AWS managed service allows to automate software deployments to a hybrid mix of EC2 Instances and On-Premises servers?

CodeDeploy


Question 2:
You are a software developer working on a project with your team. You need a secure and reliable version control system to store, share, and collaborate your code with the team. Which AWS service can help the developers?

CodeCommit

Question 3:
You need a unified user interface that gives you visibility, control, and patching capabilities for your EC2 Instances on AWS, as well as for servers running in your on-premises data centers. Which service should you use?

Systems Manager

Question 4:
A developer would like to deploy infrastructure on AWS but only knows Python. Which AWS service can assist him?

Cloud Development Kit (CDK)

Question 5:
Which of the following allows you to deploy any AWS Infrastructure as a Code?

CloudFormation

Question 6:
Which service is referred to as a Platform as a Service (PaaS)?

Elastic Beanstalk

Question 7:
What is called the declaration of the AWS resources that make up a stack?

CloudFormation Templates


Question 8:
Which of the following services can a developer use to store code dependencies?

CodeArtifact

Question 9:
Which serverless service can be used to build code and run tests?

CodeBuild

Question 10:
CloudFormation and Elastic Beanstalk are free of use.

True

CloudFormation and Elastic Beanstalk are free of use, but you do pay for the resources created