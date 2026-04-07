
# Scalability

application / system can handle greater loads by adapting

Ability to accomodate a larger load by making the hardware stronger (scale up), or by adding nodes (scale out)

## Vertical Scalability

Def -> increasing the size of the instance

Example: From running an app on t2.micro To running the app on t2.large

Very common for non distributed systems such as a database

Hardware limitations


## Horizontal Scalability

Def -> increasing the number of instances / systems for your app

Implies distributed systems

Common for web apps / modern applications

Examples:
Using Auto Scaling Group (ASG)

Load Balancer

# High Availability

Def -> running your app / system in at least 2 Availability zones

Goes hand in hand with horizontal scaling

Goal: to survive a data center loss (disaster)

Examples:

ASG for multi AZ

Load Balancer multi AZ

# Elasticity

Once a system is scalable there will be some auto-scaling -> system can scale based on load

Cloud freindly pay-per-use, match demand, optimize cost


# Agility

IT resources that are convieneint and reduces time to make those resources available to developers -> creating and deleting resources fast

# AWS OSI Layers

**Layer 7**

AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to an Amazon API Gateway API, Amazon CloudFront or an Application Load Balancer. HTTP and HTTPS requests are part of the Application layer, which is layer 7.

**Layer 3** - Layer 3 is the Network layer and this layer decides which physical path data will take when it moves on the network. AWS Shield offers protection at this layer. 

**Layer 4** - Layer 4 is the Transport layer and this layer data transmission occurs using TCP or UDP protocols. AWS Shield offers protection at this layer. 



# Load Balancing

Servers that forward internet traffic to multiple servers (EC2 instances) downstream

They spread load across multiple downstream instances

Exposes a single point of access (DNS) to your application

seamlessly handle failures of downstreams instances

High availability


# Elastic Load Balancing ELB


AWS Elastic Load Balancing (ELB) is a fully managed service that automatically distributes incoming application traffic across multiple targets,

such as Amazon EC2 instances, containers, IP addresses, Lambda functions, and virtual appliances. 

This helps you achieve high availability, fault tolerance, and seamless scalability for your applications

Does regular health checks for your instances

Spread load across multiple downstream instances

Handles failures of downstream instances

## Application Load Balancer 

best suited for HTTP and HTTPS traffic

 operates at the request level (Layer 7)

Content-Based Routing: ALBs can route traffic including the URL path (e.g., /api to one service, /images to another), hostname (e.g., app1.example.com), HTTP headers, query string parameters, or source IP address

Use Cases: Micro services, conatiner-based applications (ECS or kubernetes), serverless applications
## Network Load balancer 

Designed for extreme performance, for routing TCP and UDP traffics to target

Operates at the connection level (Layer 4)

Low latency -> handles millions of requests , with high preformance

Static IP -> Automatically gets static IP for availability zone. unlike other ALBs

Use Cases: TCP/UDP based applications, applications requiring extrem prefromance, where static-ip is mandatory, fire-wall rules, WebSocket applications requiring lobg-lived connections


## Gateway Load Balancer

Helps with deploy, scale, manage third-party virtual appliances like security appliances

Uses GENEVE protocol to encapsulate the original traffic

operates at layer 3 (network layer)

High availability and scalability: ASGs  auto scale the virtual appliances up or down based on demand

Use Cases: Manage Firewalls, intrusion detection, and prevention systems, deep packet inspections



# Auto Scaling Group ASG


Implement elasticity -> scalability fpr application across multiple 

For example: 

Load on your website and apps can change. The solution is to scale EC2 instances (removing or creating) based on demand on your systems,

replace unhealthy instances

Integrated with the ELB

## Scaling Strategies

Manual scaling: user updates the size of an ASG manually

Dynamic scaling: Responds to changing demand automatically
- Simple /Step Scaling
	- trigger is defined, and define how many units we add or remove
	- Example when CPU > 70% then add 2 units of CPU < 30% then remove 1
- Target Tracking Scaling
	- Defining a scaling policy
	- For example: defining CPU utilization to stay at around 40% on average and then the ASG will scale automatically to make sure that you stay around the target of 40%
- Scheduled Scaling
	- Anticipate a scaling based on known usage
	- Example: increase the min. capacity to 10 at 5pm on Fridays -> broadcasting a sports game
- Predictive Scaling
	-  Uses ML to predict future traffic ahead of time
	- Auto provision the right number of EC2 instances in advance
	- Useful when load has predictable time based patterns




# Quiz

Question 1:

What is the main purpose of High Availability in the Cloud?

Application thriving even in case of a disaster
High availability means applications running at least in two AZs to survive a data center loss


Question 2:

Which AWS offered Load Balancer should you use to handle hundreds of thousands of connections with low latency?


Network Load Balancer
A Network Load Balancer can handle millions of requests per second with low-latency. it operates at Layer 4, and is best suited for load-balancing TCP, UDP, and TLS traffic with ultra high performance


Question 3:

Changing an EC2 Instance Type from a t3a.medium to a t3a.2xlarge is an example of?

Vertical Scaling
Increasing the size of the instance, Changing from t3a.medium to a t3a.2xlarge is an example of size increase

Question 4:
What can you use to handle quickly and automatically the changing load on your websites and applications by adding compute resources?

An Auto scaling Group

Can automatically and quickly scale-in and scale-out to match the changing load on your applications and websites

Question 5:
Which of the following statements is INCORRECT regarding Auto Scaling Groups?

Automatically changing the EC2 instance types

Auto scaling groups can add or remove instances, but from the same type. They cannot change the EC2 instances Types on the fly


Question 6:

Which Load Balancer is best suited for HTTP/HTTPS load balancing traffic?

Application Load Balancer

Are used for HTTP and HTTPS load balancing. They are the best-suited for this kind of traffic


Question 7:

Which of the following is NOT an Auto Scaling Strategy?

Active scaling


Question 8:
Which AWS service offers easy horizontal scaling of compute capacity?

ASG

auto scaling Groups offers the capacity to scale-out and scale-in by adding or removing instance based on demand


Question 9:
Which of the following statements is NOT a feature of Load Balancers?

Back-end auto scaling

Load Balancers cannot help with back-end auto scaling. You should use auto scaling Groups 