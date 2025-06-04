It’s essentially virtual servers in cloud, could Windows, Linux, or Mac servers in cloud. It’s the basis for services like Amazon relational database service and Amazon Elastic Cash which run on EC2 instances.

## Server Virtualisation 
So a server consists of compute power which is your processor, storage,  RAM, network adapter etc. On top of that we have an OS. On top of that we install our application or service.
Limitations of Server
- OS is tied to hardware, so can’t move away OS from the hardware. 
- Leads to underutilisation of of resources
- This also leads to higher cost
- Scalability constraints
For Virtualisation, we have HyperVisor on top of the of the server. Examples of Hypervisors are VMWare, Zen, KVM and Microsoft Hyper V etc. This hypervisor creates a layer of abstraction between the physical server and what runs on top which is the virtual server or a virtual machine. It then allocates or emulates physical resources to the virtual machine. essentially gets a subset of the total resources. These Virtual machines then have their OS on top of which we can run our server or application (web service). Can be called virtual machines, virtual servers, or instances, all names for the same thing. It’s a virtual machine running atop the Hypervisor. This also then allows to run multiple “virtual servers” or instances on the same underlying physical server. These instances are also portable as not tied to the underlying physical server in the same way as without virtualisation.
Advantages of Virtual Servers (Instances)
- VM is portable 
- Better resource utilisation 
- Lower costs
- Improved scalability 
### Scaling up Vs. Scaling out
#### Stateless Applications
Eg. A weather app, it doesn’t need to record anything about user, so no “state” is recorded about user session. 
#### Stateful Application
Eg. Amazon.com for shopping, records information about user to record history, and make suggestions etc. 
for an e-commerce website, 
You have Database Server, Application Server, and then also a Web Server.
Now when you add things to the cart, they are in cookies, so since nothing about user being stored on webserver, it’s stateless. However when you make an order or purchase, then application layer process it and records data in database. Now database is stateful, as its recording info about what purchase user made. 

#### Scaling Vertically or Scaling Up 
Means adding more resources to the same instance of virtual machine. This also requires shutting down, using a software to change the configuration to add more resources and then restarting the VM.
Eg. If you have one t2.micro with one vCPU and 1GB RAM, and you want to scale up, you change it to c5.xlarge which has 4 vCPU and 8GB of RAM.
Usually done for Databases 

#### Scaling Horizontally or Scaling Out 
Means adding more instances of the stateless web service , that is having multiple instances running it, which load balance etc between them. 
Eg. Adding multiple t2.micro instances to run the application individually. 
Usually done for static web-services which are stateless.

## High Availability Vs. Fault Tolerance 
### High Availability
- minimal service interruption is the goal
- Designed with no single point of failure (redundancy)
- Uptime measured in % eg. 99.99% uptime 
- Can be synchronous or asynchronous replications. Synchronous waits for confirmation that data is received and hence slower but safer. Asynchronous on the other hand is faster as doesn’t wait for data received confirmation, but can also lead to data loss in case of failure.
- Lower cost compared to FT
- Services that create HA eg. Elastic load balancing which makes sure multiple targets are available to get hit by the requests and can also spread them across availability zones EC2 Auto Scaling ensures that enough targets are there, and replaces one if it fails. Amazon Route 53 is DNS Service.

### Fault Tolerance 
- no service interruption 
- Specialised hardware with instantaneous failover
- No downtime even if one or more components fail in the system.
- Synchronous replication 
- Examples - Fault Tolerant NICs, Disk Mirroring(RAID 1), Synchronous DB replication. 
Need multiple hard drives which have disk mirroring by RAID 1 which mirrors the writes to both simultaneously. 

## Durability vs Availability 
### Durability
It is protection against data loss, data corruption
Eg. S3 offers 11 9s Durability which translates to if you store 10 million things on s3 you can expect to lose one every 10,000 years. 
### Availability 
It is a measure of amount of time the data is available to access. Expressed as percent time per year.

 


