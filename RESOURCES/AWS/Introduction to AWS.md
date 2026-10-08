
# AWS Structure
This represents the way AWS is setup and what helps it be a global service

- AWS Regions
	- This refers to a cluster of data centers.
	- Most services are scoped to a region, and if we try using it in a new area, then its like using a new service.
	- Which region to choose :
		- Depends on compliance, like in France, data cannot leave France
		- Proximity : Which is closer to the end user
		- Availability of services : Some regions may not have the newer services.
		- Pricing : It depends on the region
- AWS Availability Zones : 
	- Each Region is composed of availability zones. Min 3 and Max 6
	- Each availability zone is one more discrete data centers which have redundant power, networking and connectivity
	- They are separate and isolated from each other. They are all connected to each other via ultra low latency networking
- AWS Points of presence
	- These are locations where it is present to provide low latency service to end users.
- NOTE : Some services are available on in certain regions, hence might need to change region to access them.