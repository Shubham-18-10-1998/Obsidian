Allows us to create users, groups, federated users and enable authentication for applications. Now all IAM principals must be authenticated to send API requests to AWS. 
Authentication happens through password to log in.
Then authorisation decides if we are allowed/denied access to resources. 
## Principal (AWS - IAM)
Person or application that can make a request for an action or operation on an AWS resource. 
## Policy
Used to decide what we have access to. Can be identity based and resource based. 
## Identity Centre 
Allows for single sign on. 
## Users
When we create an AWS account, we provide email for sign up and that creates the root user. The root user has full permissions (admin) and can’t be restricted. 
Best practice is to not use it and use Multi Factual Authentication.
Then users are created, can create up to 5000 users for one account. These have no permissions by default. 
Each user has a friendly name which is a string which can use to login with a password. There is also an associated AWS resource name.
Eg. Is Andre user created, 
Then resource name would be something like
arn:aws:iam::625158252389:user/Andrea
Arn stands for Amazon resource name, and then it shows it’s an aws resource, and iam resource followed by account number. It’s a user type of resource, and then the friendly name for it.
Can login using username and password by the console, or use access keys to login via cli or api.
One user can belong to multiple user groups and gets the combined permissions of all of the associated groups.
## User Groups
These are used to add users to them and then applying policies to them. These policies are called identity based policies and can be applied to users, groups, and roles. 
## Role
They are used to delegation and are assumed. Essentially they have permissions assigned to itself, and then you can assume the role to get those permissions. 
Each role is an IAM identity that has specific permissions.Using sts:AssumeRole can take a specific role. 
STS stands for security token service. Essentially we are logging in with certain credentials that have those, and whatever permissions that role has, we then get those. 
Once assumed, the identity essentially becomes the role and gains the role’s permissions.
## Policy
They define the permissions for the identity or resources they are associated with. 
These are documents that define the permissions, and are written in JSON.
Note: all permissions are implicitly denied by default.
Resource based policies are associated to resources like s3 buckets. Not all services do support resources based policies in AWS.