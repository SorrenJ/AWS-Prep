

when deploying multiple applications, they will need to communicate with one another 

## Synchronous communications (application to application)

Buying Service -> Shipping Service

talking directly to a service


Can be problematic if there are sudden spikes of traffic -> what if you need to suddenly encode 1000 videos but usually it's 10





## Asynchronous / Event based (application to queue to application)

Buying service -> Queue -> Shipping Service

involves a queue

anytime something is bought will put an order in a queue, shipping service will be reading from the queue to get the orders

This is decoupled

examples:

SQS -> queue model

SNS -> pub/sub model

Kinesis -> real-time data streaming model

-> can be scaled independently form out application



# SQS

Standard queue

Oldest 


Fully managed, serverless service

No need provsion servers

used to decouple applications



![[Screenshot 2026-02-14 115815.png]]


We have our web servers and they're taking request maybe through an application balancer. They're served through EC2 instances in an auto scaling group. 

And then, for example, say that our users want us to process some videos. Then instead of sending it directly to the video application, we can instead insert messages into an SQS queue, and then we will have a video processing layer made of an auto scaling group with EC2 instances.

And these EC2 instances, we'll be reading from the SQS queue and processing our videos.

The cool thing about it is that we can scale the second auto scaling group independently from the first one and this is why it's called decoupling.

And on top of it, the scaling can happen based on how many messages, for example, there are in the SQS queue.

And this would really allow us to have two layers, the web servers and the video processing fully decoupled from the SQS queue and scaling independently.

This will give us the best user experience and also the best cost efficiency and scaling concerns.

## FIFO

First In First Out (ordering of messages in the queue)

For example in a specific order such as 1,2,3,4 , the consumer will also read these messages in order

With a normal SQS queue, consumers can read messages altogether and in different order

in SQS FIFO queues the message are going to be in order


![[Screenshot 2026-02-14 124159.png]]


# Kinesis

For real-time big data streaming 

Managed service

collect, process, and analyze real-time streaming data at any scale




![[Screenshot 2026-02-14 125713.png]]


For example, when people click on your website or when you have a device that is connected to the internet or when you have metrics or logs on an application server,

then all these data points can be sent into Amazon Kinesis Data Streams and then analyzed and then, if you want to, you can also use Amazon Data Firehose to send them into destinations, such as your Amazon S3 buckets, your Amazon Redshift database and so on.


# SNS

Simple notification service

To send one message to many receivers

Event publishers will only send messages to one SNS topic, you can have as many event subscribers as you want

Each subscriber to the topic will get all the messages

Different from SQS  where consumers were sharing the messages


![[Screenshot 2026-02-14 132321.png]]

Uses a pub/sub service
-> buying services will send a message into our SNS topic
-> the topic will be smart enough to send a notification via email to the fraud service, to the shipping service, and to SQS queue














In this example, each subscriber to the topic will get all the messages sent to the SNS topic.

Each SNS topic can have more than 12 million subscriptions per topic. And also, we have a soft limit of 100,000 topic limits for each account.

So SNS has many destinations.

It can publish to many subscribers.

And from the AWS target service from SNS, we have Amazon SQS, Lambda, and Amazon Data Firehose.

But also we can send emails directly from SNS. We can send SMS and mobile notifications.

And finally, we can send data directly into a HTTP or HTTPS Endpoint.


# MQ

Is a managed message broker service for RabbitMQ  and ActiveMQ -> these are on-premises technologies that provide you access to open protocols 


Amazon MQ doesn't scale as much as SQS or SNS,



And because Amazon MQ runs on servers,

you may have server issues.


And so you can run multi-AZ setup

with a failover if you want to be highly available.

So Amazon MQ is going to be used only and only if

a company is migrating to the cloud

and needs to use one of these open protocols,

such as MQTT, AMQP, STOMP, et cetera, et cetera.

Otherwise, it should be using SQS and SNS

because they scale a lot better

and they're way more integrated

with Amazon Web Services than Amazon MQ.


# Quiz

Question 1:

A company using Apache ActiveMQ is migrating to the cloud. Which AWS service can it use to easily set up and operate its message brokers in the cloud?

Amazon MQ


Question 2:

Which service is a fully managed pub/sub messaging service that makes it easy to set up, operate, and send notifications from the cloud, using a push-based system?

Simple Notification Service (SNS)


Question 3:

You can use Kinesis to perform real-time analysis from video streams.

Amazon Kinesis indeed enables real-time analysis of video streams, allowing you to collect, process, and analyze data efficiently, which is crucial for timely insights and effective decision-making. This capability is part of its broader suite of services tailored for handling streaming data.


Question 4:
Which principle is mainly applied when using Amazon SQS or Amazon SNS?

Decouple your applications

SQS and SNS are designed to reduce dependencies between different components of an application, allowing them to function independently and enhancing system resilience. This principle supports smoother operations by ensuring that issues in one part of the system don't negatively impact others, which is crucial in distributed architectures.


Question 5:
Which service allows you to send, store, and receive messages between software components at any volume, without losing messages or requiring other services to be available, using a pull-based system?

Simple Queue

effectively facilitates communication between software components through a pull-based messaging system, ensuring message delivery without needing all services to be operational simultaneously. This decoupling is essential for building resilient and scalable applications.