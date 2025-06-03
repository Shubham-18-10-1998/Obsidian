## Global Infrastructure
- **Regions** - Each region is in a separate Geographic location.
- **Availability Zones** : Each Region consists of multiple availability zones. Can be 3 or more. Each availability zone has one or more data centre. Each availability zone has public sub-net which is accessible to the public via internet, and private subnet. Each zone has redundant power sources. Redundant Network too between the regions and within them.
- **AWS Outpost**: You can get a piece of hardware into your own data centre, this have limited capabilities and don’t offer all the services of AWS. These are connected to AWS Regions.
- **Local Zones**: These are like availability zones. Present in metropolitan areas. Slightly more expensive. Connected to a AWS region.
- **AWS Wavelength Zone**: offer 5G capability to provide low latency to mobile applications.  Connected to AWS region.
All these regions are interconnected with a network called AWS global Network.
- highly redundant, low latency, good bandwidth.

## AWS accounts
- Root user account - Admin of the account. Has all access. ideally suggested to not use this account. Now this can access IAM (Identity and access management System) to create users, groups, roles, and policies. 
- Process is create user, then create a group to put user into, then assosciate a policy that has permission to that group.
- To access, we need to authenticate IAM principals (user) through CLI, or API via SDK kit.
- We then get authorized to access certain resources via the policies.

### Policies
Define what resources we are allowed to access, and wha level of access is allowed. All identity and resources created within AWS account. Each account exists in one place and then use measure to access resources across accounts.

## AWS CloudFront 
- it’s a content delivery network. This means content (images or videos) can be cached around the world at different locations to make them available with less latency. 
Working -
CloudFront Origins -> Regional Edge Caches ->  Edge Locations -> global users 

## AWS Management Console
Allows to deploy resources (virtual servers and databases) with ease.

## AWS Shared Responsibility Model

![[image.jpg]]

![[image 1.jpg]]

## AWS Pricing Fundamentals 
- **Compute** : for cpu and ram changed based on the duration the resources are running. Per minute basis. 
- **Storage** : based on the quantity of data stored or allocated. Eg. For s3 it’s based on the amount of data stored. For ECB it’s based on amount of space allocated. 
- **Outbound Data Transfer** : Quantity of data transferred out of an availability zone or a region. 

### Pricing models 
- **pay as you go** : pay what you are using. Allows for elastic needs.
- **Save when you reserve** : invest in reserved capacity. Allows to save as much as 75 percent compared to pay as you go.
- **Pay less by using more** : volume based discounts.

## AWS Advantages 
- Trade capital expense for variable expense, that is operational expense.
- Benefit from massive economies of scale.
- Stop guessing capacity as elastic.
- Increase speed and agility. Speed is deploy resources quickly and easily. Agility is ability to react to change quickly. 
- Stop spending money on maintaining the resources like data centres etc. 
- Allowed to go global in minutes. 

## AWS Services 
[[ Identity and Access Management (IAM)]]