

# Best Practices

Scalability: vertical & horizontal

Disposable Resources: servers should be disposable & easily configured

Automation: Serverless, Infrastructure as a Service, Auto Scaling…

Loose Coupling:

Monolith are applications that do more and more over time, become bigger

Break it down into smaller, loosely coupled components

A change or a failure in one component should not cascade to other components

Services, not Servers:

Don’t use just EC2

Use managed services, databases, serverless, etc !

# Well Architected Framework Pillars
## Operational Excellence

Includes the ability to run and monitor systems to deliver business value and to continually improve supporting processes and procedures

Perform operations as code

make frequent, small reversible changes

Anticipate failure, learn from all operational failures

Strategies:

Prepare: CloudFormation, Config

Operate: CloudFormation, Config, CloudTrail, CloudWatch, X-ray

Evolve: CloudFormation, CodeBuild, Codecommit, CodeDeploy, CodePipeline





## Security

ability to protect information, systems, and assets while delivering business value through risk assessments and mitigation strategies

Strategies:

strong identity foundation - IAM -> reduce reliance on long-term credentials

Detective Controls: AWS Config, AWS CloudTrail, CloudWatch

Infrastructure Protection: CloudFront, VPC, Shield, WAF, Inspector

Data protection: KMS, S3, Elastic Load Balancing (ELB), Amazon EBS, Amazon RDS

Incident Response: IAM, AWS CloudFormation, CloudWatch Events

## Reliability

Ability of a system to recover from infrastructure or service disruptions

dynamically acquire computing resources to meet demand

mitigate disruptions such as misconfigurations

transient networks

Test recovery procedures

Strategies:

Foundations: IAM, VPC, Service quotas, Trusted Advisor

Change Management: Auto scaling, Cloudwatch, CloudTrail, Config

Failure Management: Backups, CloudFormation, S3, S3 Glacier, Route 53


## Performance Efficiency

Using computing resources efficiently to meet system requirements

maintain that efficiency  as demand changes and technologies evolve

Strategies:

Selection: auto scaling, Lambda, Elastic Block Store, Simple Storage, RDS

Review: CloudFormation

Monitoring: CloudWatch, Lambda

Tradeoffs: RDS, ElastiCache, Snowball, CloudFront


## Cost Optimization

Ability to run systems to deliver business value at lowest price point

Strategies:

Expenditure Awareness: Budget, Cost & Usage Report, cost explorer, reserved instance reporting

Cost-Effective Resources: Spot instance, Reserved Instance, S3 Glacier

Matching supply and demand: auto scaling, Lambda

Optimizing Overtime: Trusted Advisor, Cost & Usage Report


## Sustainability

Focuses on minimizing the environmental impacts of running cloud workloads


Understand your impact

Establish sustainability goals

Maximize utilization

anticipate and adopt new, more efficient hardware, and software offerings


# Well-Architected Tool

Free tool to review your architectures against the 6 pillars Well-Architected
Framework and adopt architectural best practices


# AWS Cloud Adoption Framework (AWS CAF)

organizes guidance into six areas of focus, called Perspectives. Each Perspective addresses distinct responsibilities. The planning process helps the right people across the organization prepare for the changes ahead.

## Business Perspective (CAF)

Ensures that IT aligns with business needs and that IT investments link to key business results.

Common roles:

- Business managers

- Finance managers

- Budget owners

- Strategy stakeholders


## People Perspective (CAF)

Supports development of an organization-wide change management strategy for successful cloud adoption.

Common roles:

- Human resources

- Staffing

- People managers


## Governance Perspective (CAF)

focuses on the skills and processes to align IT strategy with business strategy. This ensures that you maximize the business value and minimize risks.

Common roles:

- Chief Information Officer (CIO)

- Program managers

- Enterprise architects

- Business analysts

- Portfolio managers


## Platform Perspective (CAF)

Includes principles and patterns for implementing new solutions on the cloud, and migrating on-premises workloads to the cloud.

Common roles:

- Chief Technology Officer (CTO)

- IT managers

- Solutions architects

## Security Perspective (CAF)

Ensures that the organization meets security objectives for visibility, auditability, control, and agility.

Common roles:

- Chief Information Security Officer (CISO)

- IT security managers

- IT security analysts



## Operations Perspective (CAF)

Helps you to enable, run, use, operate, and recover IT workloads to the level agreed upon with your business stakeholders.

Common roles:

- IT operations managers

- IT support managers




## Transformation Phases

The Envision phase of the AWS Cloud Adoption Framework (AWS CAF) focuses on demonstrating how the cloud will help accelerate your business outcomes.

**Align** - The Align phase of the AWS Cloud Adoption Framework (AWS CAF) focuses on identifying capability gaps across the six AWS CAF perspectives, identifying cross-organizational dependencies, and surfacing stakeholder concerns and challenges.

**Launch** - The Launch phase of the AWS Cloud Adoption Framework (AWS CAF) focuses on delivering pilot initiatives in production and on demonstrating incremental business value.

**Scale** - The Scale phase of the AWS Cloud Adoption Framework (AWS CAF) focuses on expanding production pilots and business value to desired scale and ensuring that the business benefits associated with your cloud investments are realized and sustained.
# AWS Professional Services

a global team of experts they work alongside your team and a chosen member of the APN

## Types AWS Partner Networks

APN Technology Partners
provide hardware, connectivity, and software

APN Consulting Partners
professional services firm to help build on AWS

APN Training Partners
find who can help you learn AWS

AWS Competency Program
AWS Competencies are granted to APN Partners who have demonstrated technical proficiency and proven customer success in specialized solution areas

AWS Navigate Program
help Partners become better Partners


# AWS Managed Services

provides ongoing management of your AWS infrastructure so you can focus on your applications.

**AWS Systems Manager Session Manager**

AWS Systems Manager Session Manager is a fully-managed service that provides you with an interactive browser-based shell and CLI experience. It helps provide secure and auditable instance management without the need to open inbound ports, maintain bastion hosts, and manage SSH keys. AWS Systems Manager Session Manager helps to enable compliance with corporate policies that require controlled access to instances, increase security and auditability of access to the instances while providing simplicity and cross-platform instance access to end-users.