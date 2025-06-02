## Global Infrastructure
- **Regions** - Each region is in a separate Geographic location.
- **Availability Zones** : Each Region consists of multiple availability zones. Can be 3 or more. Each availability zone has one or more data centre.
All these regions are interconnected with a network called AWS global Network.
- highly redundant, low latency, good bandwidth.

## AWS accounts
- Root user account - Admin of the account. Has all access. ideally suggested to not use this account. Now this can access IAM (Identity and access management System) to create users, groups, roles, and policies. 
- Process is create user, then create a group to put user into, then assosciate a policy that has permission to that group.
- To access, we need to authenticate IAM principals (user) through CLI, or API via SDK kit.
- We then get authorized to access certain resources via the policies.

### Policies
Define what resources we are allowed to access, and wha level of access is allowed. All identity and resources created within AWS account. Each account exists in one place and then use measure to access resources across accounts.
