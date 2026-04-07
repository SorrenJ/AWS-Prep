
# CloudWatch

CloudWatch have metrics for every service, seen in the Cloudwatch dashboard

a metric is a variable to monitor (CPUUtilization, NetworkIn)

With CloudWatch Events, you can establish rules that trigger programmatic actions in response to a change in volume, snapshot, or encryption key state (though not for underutilized volume usage).


Metrics have timestamps

![[Pasted image 20260217133615.png]]



Important Metrics

EC2 instances: CPU Utilization, status checks, network

EBS volumes: Disk Read/Writes

S3 buckets: BucketSizeBytes, NumberOfObjects, AllRequests

Billing: Total estimated charge (only in use-east-I)

Service Limits: how much you've been using a service API

Custom metrics: push your own metrics

## CloudWatch Alarms

alarms used to trigger for any metric

Alarm happens...

Auto scaling: increase or decrease EC2 instances "desired" count

EC2 actions: stop, terminate, reboot, or recover an EC2 instance

SNS notifications: send notification into SNS topic

Can create your own alarm, i.e. billing period

## CloudWatch Logs

Enables real-time monitoring of logs from Elastic Beanstalk, ECS, AWS Lambda, CloudTrail, EC2, on-premises servers, Route53 DNS queries

By default, no logs from EC2 instance will go to CloudWatch, you need to run a Cloudwatch agent on EC2 to push the log files you want. Can also be setup on-premises too


# EventBridge

is a serverless event bus that enables you to connect applications together using events

a service that provides real-time access to changes in data in AWS services, your own applications, and software as a service (SaaS) applications without writing code. Amazon EventBridge Scheduler is a serverless task scheduler that simplifies creating, executing, and managing millions of schedules across AWS services without provisioning or managing underlying infrastructure.


soureces can be many things

Schedule Cron jobs through scheduled scripts

Contains event busses as it's main pathaway for events. they are like dedicated channel that recieve and route events

You can write a schema registry to model the event schema -> to see the data types

Archive events

Types of event buses

Default Event -  events happening from within AWS Services, or, for example, your schedules.

Partner Event - Events outside of AWS that are partnered with AWS For example, if you're using Zendesk, or Datadog, then they can send their own events into your account through a partner event bus

Custom Event -  write any kind of integration you want and be really able to customize everything.

![[Product-Page-Diagram_Amazon-EventBridge-Scheduler.ab2cc1a1c0f233a4e1e4c5829a0d6c5fc23d9586.png]]
# CloudTrail

Provides governance, compliance and audit for your AWS Account

How would we know what has been deleted and who deleted it and when? Then the answer is going to be CloudTrail.

 to log, monitor and retain account activity related to actions across your AWS infrastructure. CloudTrail provides an event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command-line tools, and other AWS services.
 
Get an history of events / API calls made within your AWS Account by:
• Console
• SDK
• CLI
• AWS Services

for audit and security purposes you can take the logs of all the history of events and API calls made within CloudTrail and send them to two locations, either CloudWatch Logs or Amazon S3.

# X-Ray


Helps developers analyze and debug, troubleshooting distributed applications

Preforms a tracing (a collection of data points sharing a unique trace ID,  representing a single request as it travels through your application) and gets a visual analysis of your application

Once enabled on your services, then you'll get a full picture of what is happening for each service

See where they're failing, their performance  and if one request goes wrong you will be able to visualize it

![[Screenshot 2026-02-18 132632.png]]

Advantages
- Troubleshooting performances through bottlenecks (specific causes of performances issues)
- Understand dependencies in a microservice architecture ( ) 
- pinpoint service issues
- review request behavior
- find the errors and exception for that request
- If you are meeting service level agreements (SLA)
- Where I am throttled (if we're being slowed down, where is it happening, in which service?)
- Which users are going to be impacted by these outages

# CodeGuru

ML powered service for automated code reviews and application performance recommendations

Functionalities

- CodeGuru Reviewer: automated code for statics code analysis -> development
	- Built-in code reviews with actionable reccomenations
	- Identify critical issues, security vulnerabilities, hard to find bugs
	- common coding best practices, resource leaks, security detection
	- integrates github, bitbucket, aws codecommit
- CodeGuru Profiler: Analyzes application runtime behaviour to find performance bottlenecks -> production
	- Detects and optimize the expensive lines of code in pre-prod
	- identify performance and cost improvments in production
	- helps understand the runtime behaviour
	- identify and remove code inefficiencies
	- decrease compute costs
	- anomaly detection
	- support on-premise applications
# Health Dashboard

## Your Account

Account health dashboard provides alerts and remediation guidance when aws is experiencing events that may impact you

Gives a personalized view into the performance and availability of your AWS services in your resources

displays relevant and timely information to help manage events and progress

provides notifications to help plan for scheduled events

Shows how AWS outages directly impact you and your aws resources

## Service

Displays general status of AWS services

Shows all regions, all services health

Show historical health for each day

Service health is the single place to learn about the availability and operations of AWS services. You can view the overall status of AWS services, and you can sign in to view personalized communications about your particular AWS account or organization.

Service health offers the possibility to subscribe to an RSS feed to be notified of interruptions to each service.
# Quiz

Question 1:
Which CloudWatch feature would you use to trigger notifications when a metric reaches a threshold you specify?

CloudWatch Alarms

Allows you to watch CloudWatch metric and to recieve notifications when the metrics fall outside of the levels (high or low thresholds) that you configure

Question 2:

Which AWS service helps developers analyze and debug production as well as distributed applications?

X-Ray

Helps developers analyze and debug production, distributed application such as those built using a microservices architecture

Question 3:

Which AWS service provides alerts and remediation guidance when AWS is experiencing events that may impact you?

AWS Account Health Dashboard

Provides alerts and remediation guidance when AWS is experiencing events that may impact you


Question 4:
You need to set up metrics monitoring for every service in AWS. Which service would you use?

CloudWatch 
is monitoring service for AWS cloud resources and the applications you to run on AWS. You can use it to collect and track metrics, collect and monitor log files, and set alarms



Question 5:
Which service allows you to inspect, audit, and record events and API calls made within your AWS account?

CloudTrail

A web service that records activity made on your account and delivers log files to your Amazon S3 bucket.  This enables governance, compliance, operational auditing and risk auditing

Question 6:
Which AWS service automatically analyzes code and provides performance recommendations?

CodeGuru is a developer tool provides reccomendations to improve code quality and identify an application's expensive lines of codes


Question 7:
How would you describe Amazon CloudWatch Logs?

A single, highly scalable service that centralizes the logs from all of your systems, applicatuions, and AWS services that you use

Question 8:
If a resource is deleted in AWS, which service should you use to investigate first?

CloudTrail

can record the history of events/API calls made within your AWS account, which will help determine who or what deleted the resource. You should investigate it first


