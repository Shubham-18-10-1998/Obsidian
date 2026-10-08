# Introduction

- Stands for Identity and Access Management System.
- Helps us to create our users and assign them to a group.
- The root account shouldn't be used or shared.
- Groups can only contain users, not other groups
- User can also not belong to any group, or belong to multiple groups.
- Why do we need Users and Groups ?
	- Cause we want the users to be able to use the aws account and to do that we have to give them permissions
- Working : 
	- Users and Groups can be assigned JSON documents called policies.
	- Policies define the permissions for a user.
	- Least privillege, dont give more permissions than needed.