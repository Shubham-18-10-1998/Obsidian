## Introduction
- Allows us to create users, groups, federated users and enable authentication for applications.
- All IAM principals must be authenticated to send API requests to AWS. 
- Authentication happens through password to log in.
- Then authorisation decides if we are allowed/denied access to resources. 
- Even IAM allows SSO to was services by federating with external idPs.
## Principal (AWS - IAM)
Person or application that can make a request for an action or operation on an AWS resource. 
## Policy
Used to decide what a user or a role which has that policy will have access to. Can be identity based and resource based. 
## Identity Centre 
- Allows for single sign on. 
- Enables centralised permissions management and SSO.
- Identity sources can be Identity Centre directory, Active Directory and standard providers using SAML 2.0
- Can use AD to connect to for example Azure AD or to connect to on Prem Active Directory, use AD connector plugin, or AWS Managed Microsoft AD.
- Also has built in SSO integration for many business applications like GitHub, Dropbox, Confluence etc.
- Provides SSO to account parts of an AWS organisation.
## Users
- When we create an AWS account, we provide email for sign up and that creates the root user. The root user has full permissions (admin) and can’t be restricted. Best practice is to not use it and use Multi Factual Authentication.
- Then users are created, can create up to 5000 users for one account. These have no permissions by default. 
- Each user has a friendly name which is a string which can use to login with a password. There is also an associated AWS resource name. Eg. If Andre user is created, then resource name would be something like : arn:aws:iam::625158252389:user/Andrea
	'arn' stands for Amazon resource name, and then 'aws' shows it’s an AWS resource, and 'iam' shows its an IAM resource followed by account number. 'user' shows its a user type of resource, and then followed by the friendly name for it.
- Can login using username and password by the console, or use access keys to login via cli or api.
- One user can belong to multiple user groups and gets the combined permissions of all of the associated groups.
## User Groups
These are used to add users to them and then apply policies to them. These policies are called identity based policies and can be applied to users, groups, and roles. 
## Role
- They are used for delegation and are assumed. Essentially each role has permissions assigned to itself, and then you can assume the role to get those permissions. 
- Each role is an IAM identity that has specific permissions.Using sts:AssumeRole can take a specific role. STS stands for Security Token Service. Essentially we are logging in with certain credentials that have those, and whatever permissions that role has, we then get those. 
Once assumed, the identity essentially becomes the role and gains the role’s permissions.
Trusted Entity while creating a role refers to who is able to assume that particular role. 
A new account created cannot assume role in the starting too, cause it doesn’t have permission.
So this was we can give access to an account to perform actions to which it doesn’t have access, by temporarily assuming the role when needed.
## Policy
- They define the permissions for the identity or resources they are associated with. 
- These are documents that define the permissions, and are written in JSON.
- Note: all permissions are implicitly denied by default for users other than the root user which has admin access.
- Resource based policies are associated to resources like s3 buckets. Not all services support resources based policies in AWS.