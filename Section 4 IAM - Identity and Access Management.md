
## Groups and users

Groups -> Users 


IAM is Identity and Access Management

## Users
are people within your organization, and can be grouped
Users don't have to belong to a group, and users can belong to multiple groups


Access keys are long-term credentials for an IAM user or the AWS account root user. You can use access keys to sign programmatic requests to the AWS CLI or AWS API (directly or using the AWS SDK


### Root User

**Root user access credentials are the email address and password used to create the AWS account**

**It is highly recommended to enable Multi-Factor Authentication (MFA) for root user account**

The Email address and the password used for signing up for AWS services are the AWS root user account credentials. Root user account, therefore, has full permissions on all AWS resources under that account. Restricting root user account access is not possible. As a best practice, Multi-Factor Authentication (MFA) should be set on the root user account. The root user account password can be changed after account creation. For all employees performing various administrative jobs, create individual user accounts using AWS IAM, and give administrative permissions as needed.
## Groups 

An IAM User Group is a collection of IAM users. Groups let you specify permissions for multiple users, which can make it easier to manage the permissions for those users.

only contain users, not other groups


IAM Permissions
![[IAM user and group.png]]

Tells us what a user is allowed to do or what a group and all the user can do


<div style="page-break-after: always"></div>
### CloudWatch Permissions

Users or Groups can be assigned JSON documents called policies. These policies define the
permissions of the users

``` json

{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Action": "ec2:Describe*",
			"Resource": "*"
		},
	{
		"Effect": "Allow",
		"Action": "elasticloadbalancing:Describe*",
		"Resource": "*"
},
{
		"Effect": "Allow",
		"Action": [
			"cloudwatch:ListMetrics",
			"cloudwatch:GetMetricStatistics",
			"cloudwatch:Describe*"
		],
		 "Resource": "*"
		}
	]
}
```

This allows our users to use some services in AWS,  these policies will help define permissions of our users

You don't want users to do everything, ->they could launch so many services -> cost alot of money or a threat to security

You should apply Least Privilege Principle -> don't give more permissions than a user needs

IAM Policies Inheritance

Group Level Policies
The policy will get applied to every single member of the group

Inline policies
Policy only attached to a user. User could or could not belong to a group





# Policies
### IAM Policies Structure


![[Pasted image 20251001145459.png]]

#### Structure
Version: policy language version, always include “2012-10-17”
 
 Id: an identifier for the policy (optional)

 Statement: one or more individual statements (required)

#### Statement
Sid: an identifier for the statement (optional)

Effect: whether the statement allows or denies access
(Allow, Deny)

Principal: account/user/role to which this policy applied to

Action: list of actions this policy allows or denies

Resource: list of resources to which the actions applied to

Condition: conditions for when this policy is in effect
(optional)

### Adding permissions to a user

![[Screenshot 2025-10-01 153151.png]]



![[Screenshot 2025-10-01 153345.png]]


![[Screenshot 2025-10-01 153433.png]]


<div style="page-break-after: always"></div>

### Creating a group

As Stephane, when you go into user groups and try to create a group, what happens?

![[userGoup1.png]]


As a result you cannot create it because the user Stephane is not allowed to CreateGroup

![[userGroup2.png]]

So let's create a group as Admin user, and add the user: `stephane` by checking the box

![[userGroup3.png]]


then Attach a policy and then press Create group

![[userGroup4 1.png]]

Now the `developers` group is created
![[userGroup5.png]]

Go to Admin group

![[userGroup6.png]]

Add a user to group

![[userGroup7.png]]

Add user: `stephane` to admin group

![[userGroup8.png]]


Go to IAM -> Users -> `stephane`



![[userGroup6.5.png]]

In `stephane`, scroll down to permissions policies, you can see `stephane` now has 3 policies, `AdministratorAccess` inherited from `Group admin`, `AlexaForBusiness` inherited by `developers`, and `IAMReadOnlyAcesss` attached directly

![[userGroup9.png]]

### Deep dive into policies

Let's look at `AdministratorAccess` policy

![[policies1.png]]![[policies2.png]]



![[policies3 1.png]]

Here are the services that have full permission. 

But how are they defined?


![[policies4.png]]

If you click on JSON, we get the JSON form of this policy

![[policies5 1.png]]

Let's take a look at how the `Statement` is defined

This means that a permission is allowed

```json
"Effect": "Allow"
```


 `Action` with a `*` means -> any or all actions. So altogether it means any permissions are allowed
```json
"Action": "*"
```

Any resource is allowed, is the same as giving administrator access to someone

```json
"Resource": "*"
```


Let's look at another policy: `IAMReadOnlyAccess`

![[policies6.png]]


![[policies7.png]]

`Action` contains all the api calls that are allowed like `iam: GenerateCredentialReport`

for `"iam:Get*"` -> the * means anything that starts with Get and something after is authorized. For example, get users, or get groups

By using a `*` we encompass and group many API calls together

All of api calls in `Action` are allowed on `Resource: *`

<div style="page-break-after: always"></div>

### Creating your own Policy

Go to IAM > Policies > Create policy

![[createPolicy1.png]]


![[createPolicy2.png]]

Click JSON to view the policy editor



![[createPolicy3.png]]

Search and find the Actions that should be allowed, suchas ListUsers, and GetUser

![[createPolicy4.png]]
![[createPolicy5.png]]

After clicking next you can enter the name of the policy and the description. 

![[createPolicy5.5.png]]


At the bottom you can click Create Policy

![[createPolicy6 1.png]]


Now you can go to IAM > Policies 

To see your policy that you just created. 


![[createPolicy6.5.png]]
![[createPolicy7.png]]




# How can users access AWS ?

To access AWS, you have three options:
• AWS Management Console (protected by password + MFA)
• AWS Command Line Interface (CLI): protected by access keys
• AWS Software Developer Kit (SDK) - for code: protected by access keys

• Access Keys are generated through the AWS Console
• Users manage their own access keys
• Access Keys are secret, just like a password. Don’t share them
• Access Key ID ~= username
• Secret Access Key ~= password


In the management console this is the access key

![[Pasted image 20251002161024.png]]

## AWS Management Console

This is a simple web interface for accessing AWS services.

On top of strong passwords you need an MFA for AWS

MFA is using the combination of a password that you know and a security device that you own

This prevents any IAM users from accessing your account which they can possibly change configs or delete resources, and protects Root Account and IAM users

Main benefit of MFA:

if a password is stolen or hacked, the account is not compromised


### MFA device options

#### Virtual MFA device

Support for multiple tokens on a single device

 - Google Authenticator

- Authy


#### Universal 2nd Factor (U2F) Security Key

Support for multiple root and IAM users using a single security key

- YubiKey


#### Hardware Key Fob MFA Device

#### Hardware Key Fob MFA Device for AWS GovCloud (US)



## AWS CLI

A tool that enables you to interact with AWS services using commands in
your command-line shell. You get direct access to the public APIs of AWS services and can develop scripts to manage your resources.

This is an alternative to using the AWS management console

It’s open-source https://github.com/aws/aws-cli



![[Pasted image 20251002164610.png]]
### 1. Retrieve Access Keys

![[retrieveAcessKeys.png]]

### 2. Configure AWS CLI

``` bash

aws configure

AWS Access Key ID [None]: <Access key ID>

AWS Secret Key Key [None]: <Secret access key>

Default region name [None]: eu-west-1

Default output format [None]:


```


List the users that has permissions

``` bash

aws iam list-users
```

### AWS CloudShell

Similar to AWS CLI but it's now on the AWS site. It's only available for some regions

Contains it's own full repository

![[awsCloudShell.png]]



## AWS SDK

 AWS Software Development Kit (AWS SDK),  Language-specific APIs (set of libraries). 
 
 Enables you to access and manage AWS services programmatically. But this time the SDK is NOT something that you use within your terminal, instead it is something that you embed within your application that you have to code.
 
 Embedded within your application

Supports SDKs (JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node.js,
C++) , Mobile SDKs (Android, iOS, …), IoT Device SDKs (Embedded C, Arduino, …)

Example: AWS CLI is built on AWS SDK for Python



# Roles

 An IAM role is similar to an IAM user, in that it is an AWS identity with permission policies that determine what the identity can and cannot do in AWS. However, instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it.

A role is a way to to give AWS entities permissions to do stuff on AWS

Some AWS service will need to perform actions on your behalf To do so, we will assign permissions to AWS services with IAM Roles

Common roles: EC2 Instance Roles, Lambda Function Roles, Roles for CloudFormation

## Creating a role


You can create more than one role

![[creatingARole-1.png]]


You select the role type. We select AWS service for EC2, Lambda, etc


![[creatingARole-2.png]]


At bottom we also select a Use Case, we choose EC2 since we want to create a role for that service, and click Next




![[creatingARole-3.png]]


Now the role has been created but we must add a permission. We are going to attach the IAM read only access to allow the EC2 instance to read whatever is in IAM

![[creatingARole-4.png]]



After this we name the role and we can write a description.


![[creatingARole-5.png]]


We can check the trusted entities. This defines the role for the EC2 service

![[creatingARole-6.png]]

The we can verify the permissions to check if it has the IAM read only access, and yes it does so we click Create Role

![[creatingARole-7.png]]


Now the role is created, and we can see it now in the list

![[creatingARole-8.png]]



# Security Tools

## IAM Credential Report (account-level)

A report that lists all your account's users and status of their various credentials



![[credReport-1.png]]



![[credReport-2.png]]


We can see when the user was created, if the password was enabled, when the password was last used and last changed, when is the next rotation to be expected if we do enable password rotation? Is MFA active?


## IAM Access Advisor (user-level) AKA Last Access

Access advisor shows the service permissions granted to a user and when those
services were last accessed. You can use this information to revise your policies.

![[acessAdvisor-2.png]]


 If a user accesses a specific service for example Amazon EC2, we are told that this is the administrator access that granted this service

Access Advisor becomes very helpful when you need to do granular user access permissions on AWS.



# IAM Guidelines & Best Practices

Don’t use the root account except for AWS account setup

One physical user = One AWS user -> So if a friend of yours wants to use AWS, do not give them your credentials, instead, create another user for them.

Assign users to groups & assign permissions to groups -> make sure security is managed at the group level

Create a strong password policy

Use / enforce MFA -> to guarantee your account is going to be safer from hackers

Create and use Roles for giving permissions to AWS services -> that includes EC2 instances, virtual servers

When using AWS programmatically or using CLI  or SDK, you must generate access keys

Audit permissions of your account using IAM Credential Report & IAM Access Advisor

Never Share IAM users & Access Keys


<div style="page-break-after: always"></div>

--------------------------------------------------------------------------
# Shared Responsibility Model for IAM


What **YOU** are responsible for:

- Users, Groups, Roles, Policies management and monitoring

- Enabling MFA on all accounts and enforcing this

- Rotating your access keys often

- Use IAM tools to apply appropriate permissions

- Analyzing access patterns & reviewing permissions

What **AWS** is responsible for:

- Infrastructure (global network security)

- Configuration and vulnerability analysis

- Compliance Validation

