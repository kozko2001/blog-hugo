
---
title: AWS certified solution architect associate
date: 2022-05-08 00:00:00
---
---

# AWS certified solution architect associate

* **Region**: is a geographical zone that have a at least two AZ who are autonomous from each other.
* **AZ (Availability Zones)**: a datacenter, in a region, with all that needs to be able to run the services
* **Edge locations**: small servers all around the world, that serve content from CloudFront for geo caching.

## 1 IAM

* Users: A user, they will not have access to the console if we don't check the option
* Groups: group of user that inherit the policies of the group
* Roles: services in AWS can have roles, that have policies allowing to access to some services
* Policies: actual permissions allowing or denying access to a resource
* Always AWS give least possible privilege 
  * New created users will have 0 permissions by default

### IAM Policies
#### ARN
- amazon resource name begins with `arn:partition:service:region:account_id:`
	- partition => aws or something in china
	- service => s3, ec2, rds
	- account_id 12 digit 
- example
	- `arn:aws:iam::123456789012:user/mark`
	- `arn:aws:iam:::bucket/image.png`
	- `arn:aws:dynamodb:us-east-1:123456789012:table/orders`

We have 2 types of IAM policies
- Identity policy => attach to user/group or role
- Resource policy -> attach to a resources ie( s3 bucket etc...)

Policies:
```json
{ 
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Name of the statement",
			"Effect": "Allow or Deny",
			"Action": [
				"dynamodb:Get*" // Api call name
			],
			"Resource": "arn:aws:dynamodb:*:*:table/MyTable"
		}
	]
}
```

For S3 we need normaly 2 statements:
- one with `s3:ListBucket` + resource = `arn:aws:s3:::bucket-name`
- one with `s3:Get/PutObject` + resource = `arn:aws:s3:::bucket-name/*`

- everything is implictly denied
- if there is a policy that denies  => will deny always => no matter another allows

### Permission boundaries
- allow to delegate adminstration to other users
- allow other users create IAM policies/roles in without unnecessarily broad permissions

### AWS Resource Access Manager RAM
- to share resources between accounts (individual or organizations)

### AWS Signle Sign-On
- allow you to login into AWS with google/salesforce/github etc...
- SAML 
- define permissions 

### AWS Directory Service

Multiple services

#### AWS Managed Microsoft AD
- can have Trust -> you can connect the cloud AD to a on-premise AD
- managed by AWS (except for users/groups/policies)
- MultiAZ for HA and performance

#### Simple AD
- Basic AD
- between 500 and 5000 users
- no Trust => you cannot join to your on-premise AD

#### AD Connector
- proxy to on-promise AD
- allow to log in AWS using AD
- you can join EC2 instances to an existing AD domain


#### Cloud Directory
- ????

#### Cognito User Pools
- Sign-up sign-in for web or mobile apps
- manager user directory for SaaS applications

## 2. S3

* Files can have up to 5Tb
* universal namespace -> bucket names have to be unique -> url
* Objects
  * Key => filename
  * Value => content of the file
  * Version ID =>
* You can protect S3 files => making MFA need for delete files

### Guarantees

* Build for 99.99% availability
* Amazon guarantees 99.9 availability
* amazon guarantees 11 9's durability

### Consistency

* Read after write for PUTS of new Objects
* Eventual consistency (secs) for overwrites and deletes

### Storages Classes

* S3 Standard 99.99 availability - 11 9's durability
* S3 - IA (Infrequently accessed) - instant access but rapid access => low fees but charged a retrieval fee
* S3 One Zone - IA =>
* S3 - Intelligent tiering => ML moving the tiers depending how much you use
* Glacier => takes minutes/hours to retrieve the object
* Glacier Deep Archive => 12 hours

### Costs

* Storage
* num of request Request
* depending on the tier
* Data transfer
* Transfer acceleration
* Cross region replication => use edge location and use amazon backbone network

### Security

* Bucket policies
* Access Control Lists (policies inside the S3)

### Encryption

* Encryption in Transit (SSL/TLS)
* Encryption at rest (SSE -> Server Side Encryption)
  * S3 Managed keys - SSE-S3
  * AWS Key Management server - SSE-KMS
  * Server Side Encryption with Customer Provided Keys - SSE-C
* Client Side Encryption

### Lifecycle

* Transition current version of objects between storage classes
* transition previous version of objects between storage classes
* Expire current versions of objects
* permanently delete previous versions of objects

### Object Lock

WOTM (Write once, read many) => unmodifible and undeletable during a retention period

* Governance mode => some users can delete the files
* Compliance Mode => no user, even root user can overwrite or delete the file

### S3 Performance

* latency of around 100/200 ms first bites
* if you use SSE-KMS => limits of KMS quota
* Multipart uploads (mandatory for 5B files)
* Byte-Range fetches
  * Split the request into different offset
* Requests
  * 5.500 GET/HEAD per sec per prefix
  * 3.500 PUT/COPY/POST/DELETE per sec per prefix
  * if you have files in different prefix's (folders) you can get better performance

### S3 Select

Pull information from S3 using SQL

Imagine you have CSV file in S3, and you need only some specific rows => instead of download the whole CSV => you ask S3 select to download a subset of the data you need

### S3 across accounts

* IAM + S3 bucket policies (whole bucket)
* IAM + S3 ACL (single files)
* Cross-account IAM Roles
  * **on account a**: Create a new role (with Trusted entity == Another AWS Account) with a policy to have access S3
  * **on account b**: create a new user

### S3 cross-region replication

\-> need versioning for to work -> once create replication lifecycle -> only applies to new objects or updates of the objects

### AWS Data Sync

* Allow you to move a large amount of data to AWS
* normally from a data center => install AWS DataSync agent => S3, EFS,
* you can use it for EFS to EFS

### Snowball

To move really big amount of data.

They send you a device that you can fill with data, and sent it back to AWS. The data is added to a S3 bucket you chose

### Storage Gateway

is a VM machine image agent to send data to AWS. Main purpose to sync data from on-promise datacenter to cloud

* FileGateway: for flat files -> stored directly to S3
* VolumeGateway:
  * Stored volume: your data is in the on-premise machine => but there is a replica in S3
  * Cached volume: Your data is on S3, and the most used data is cached on-premise
* GateWay Tape library => backups from physical tapes

## 3. AWS Organization

Allow you to organize different AWS accounts into an organization that you created and centrally manager

Allow you to place policies to each OU (Organization Units) => that will go down to AWS Accounts

## 4. Athena

Allow you to query S3 as if it was a database (S3) => cost by query and by scanned files

Typical use case => find logs

## 5. Macie

Security service that can scan s3 files and log trails etc... searching for PII data

## 6. EC2

Service that provides resizable compute capacity in the cloud. the time to create/reboot is in minutes scale. Which allows quick scaling.

### Pricing models

* On demand -> pays fixed rate by the hour with no commitment
* Reserved -> Capacity reservation => 1 year => lower price
* Spot instances -> Exces capacity of EC2 => drop the prices =>the price moves around => you set the price you want to bid
* Dedicated Hosts => Physical EC2 => use case special licensing ie. Oracle DB

### Instance types

* F1 => FPGA => chips to reprogram
* I3 => High speed storage => NO SQL
* G3 => Graphics intensive =>Video Encoding, 3D apps
* H1 => High Disk throughpot => Map reduce workloads, distribute file systems
* T3 => Lowest cost general purpose => WebServers, Small DBS
* D2 => Dense storage => FileServer /Hadoop
* R5 => Memory Optimized
* M5 => General purpose
* C5 => Compute optimized
* P3 => GPU => Bitcoin, ML
* X1 => Memory optimized => Spark
* Z1D => High compute and memory
* A1 => ARM => scaleout workload (ie. WebServers)

numbers -> are the generation they might change

### Security groups

\-> you can block specific port or ip => everything is blocked by default -> changes in SG are effective immediately

\-> if we create an inbound rules => automatically a outbound rule will be create

### EBS

EBS => Elastic block store => Harddisk in the cloud => automatic replication in the AZ

* General purpose (SSD):
  * Most workloads
  * gp2
  * 1Gb-16Tb
  * 16k IOPS
* Provisioned IOPS
  * Databases
  * io1
  * 64 IOPS
* Throughput Optimised
  * low cost
  * big data - Data warehouses
  * st1
  * 500 IOPS
* Cold HDD
  * Lowerst cost
  * File Servers
  * sc1
  * 250 IOPS

### AMY Types

* EBS => use an EBS as a template root storage, you can stop the machine and resume.
* Instance Store => the template root disk is in S3 => you can not stop the machine

### ENI vs ENA vs EFA

* ENI (Elastic Network Interface) => virtual network card
* EN (Enhanced Network) => Uses singe root IO virtualization (SR-IOV) to provide high performance networking
  * more performance that ENI
  * SR-IOV is a way to virtualize with more speed of IO and use lower CPU
  * your AWS instance type has to support
  * no more cost
  * 100Gbps
* EFA (Elastic Fabric Adapter) =>a network device that you can attach to your AWS EC2 to accelerate High performing computing and ML apps
  * only linux

### Spot Instance and Spot fleet

* allow you to take advantage of not used EC2 capacity
* 90% of discount
* You decide the max bid price
* Spot block -> allow you to block to go down even if the price is going up your price for 1hour to 6 hour
* you can request to be persistent => if the price get higher => the machine will be "stopped" and resumed when the price is below again

Spot fleets: collection of spot instances and optionally on-demand instances

### EC2 Hibernate

\-> when stopping the instance => we ask the host OS to hibernate (bulk ram to disk) => the disk is an EBS. -> when the machine is resumed => it ways faster -> will retain the instance ID

### IAM Roles

* allow to attach policies to AWS resources (like EC2) -> to give them permission to do specific actions on other AWS resources

### Bootstrap scripts

Way to automate EC2 instances, to run specific commands when the EC2 starts

### Instance metadata

for bootstrap scripts `curl http://169.254.169.254/latest/user-data`

get the local ip = `curl http://169.254.169.254/latest/meta-data/local-ipv4`

### EFS

Elastic File System => is a file storage service for EC2. with Elastic capacity => get more/less capacity as you add/remove files

You can not have 2 EC2 instances sharing an EBS volume, but you *can* have them sharing an EFS

Great for fileserver or to share beween EC2 instances.

* Linux only

it's actually a NFSv4 mount, you need to mount it into linux and install some tools

across multiple AZ within a region Read after write consistency

### FSx for Windows

* AWS managed windows server to file server (SMB
* Supports Active directory

### EC2 Placement Groups

Strategies for having EC2 instance in different machines or not. For availability vs performance

3 types:

* Clustered placement
  * a grouping of instances within a single AZ
  * low network latency
  * not all instance types can be in clustered placement group
* Spread placement
  * Each EC2 instance is going to be locate in different underlying hardware
  * so if the hardware fails other instances should be fine
  * you can configure them to be in the same or different AZ
* Partitioned placement
  * combination of both...
  * you define partition
    * each instance is in the same machine/rack
  * each partition is sure into different machine/rack

## 7. AWS WAF

Web AWS firewall

Can monitor HTTP/HTTPS => can look at the http petitions (querystring, url, post data) etc...

* Cloud front or API Gateway
* Can block IP addresses, country, value in request header, values in strings (even regex)
* presence of SQL code
* presence of XSS

## 8. Databases

- Multi AZ -> disaster recovery
- Read replicas -> for performance => 5 copies?

- Amazon aurora => amazon own proprietary database
- dynamodb => document /key-value noSQL db.
- redshift => amazon OLAP system => business analytics

### Backups / MultiAZ / Read Replicas

### RDS Backups
- automated backups: 
	- retention time: max 35 days
	- enabled by default
	- backup data is stored S3 (free)
- snapshot
	- done manually (user trigger)
- on restore => will have a new rds instance => new rds url
- if encryption is enabled => backups are also encrypted

### RDS Multi AZ
- in event of planned db maintenance, db instance failure or AZ failure
- the RDS endpoint will failover  the a new AZ
- where there will be a replica of the main db
- for disaster recovery (**DA**) only

### RDS Read Replica
- you have another database replica (for only read) in the same AZ
- so you can balance requests queries to both RDS
- used for scaling not DA
- you can have up to 5 replicas
- you can have read replicas in separate region
- if you promote a read replica to it's primary RDS => replication stops

### DynamoDB 
- document and key-value data models
- NoSQL
- stored in SSD
- Spread accross 3 AZ
- 2 consistency models
	- **Eventual consistent Reads** => not guarantedd Read after write => around 1 sec => best performance
	- **Strong consistent Reads** => guaranteed read after write

### DynamoDB Accelerator (DAX)
- managed, in memory cache
- 10x performance cache
- it creates a transparent proxy of dynamodb with cache (think like a redis/memcache)

### DynamoDB Transactions
- you can define transactions in dynamodb => if some write fail, all write fails
- upto 25 items or 4Mb
- you use a little bit more write/read 

### DynamoDBN On Demand capacity
- more expensive
- it acomodates to your read/write capacity
- useful, if you don't know how much provisioned capacity do you need

### DynamoDB Point in time recovery
- you can recover at any point in the last 35 days
- not enable by default

### Dynamodb streams
- stored for 24hours

### DynamoDB Global Tables
- Multi region => Disaster recovery or High Availability
- sync in under 1 sec between regions

### RedShift
Business intelligence in the cloud
is a columnar database => better compressions


configurations:
- single node: max 160Gb
- Multi node
	- leader node => manags client connections and queries
	- compute node => up to 128 

Pricing: compute node hours + backups + data transfer

- only 1 AZ

### Aurora 
Amazons own proprietary DB
- compatible with MySQL and PostgreSQL
- thought for speed and high availability
- cheaper than postgresql or mysql and faster
- autoscales disk
- upto 15 read replicas => latency of ms

Aurora Serveless => is like autoscaling database, based on the usage will scale the capacity of the db cluster

###  ElasticCache

memcache / redis

- redis is multiAZ

### Database Migration Service  (DMS)
Helps you migrate database data to the cloud, to on promise, or between cloud

- its a server in AWS
	- that replicates a source database, to a target database
	- creating the schemas and data missing

supports
- homogenous migrations ie => from oracle db to oracle db
- heterogeneous migrations ie => from oracle to aurora db
- the target, doesn need to be a database, can be S3, kinesis, dynamodb, elasticsearch service

### EMR Elastic Map Reduce
3 times faster of Spark

## R53

Types of DNS entries

- A => name to IP
- cname => name to another name
- alias => name to a AWS resources

- Top Level domain `.com` `.es`  
- `.co.uk` `.uk` is the top domain `.co` is the second level domain name


### R53 Routing policies

- Simple routing policy => one record with multiple ip addr, in a random order
- Weighted routing policy => one record, multiple ip addr, random based on weights
- latency based policy => route trafic basic on best latency for the user => basically routing to the best region
- failover policy => multiple ip, the active is the normal one, we use a healthcheck to know the health of our endpoints => if the service is unhealthy => we go to another region
- geolocation policy => where we send based on the geographic information of our users
- geoproximity routing => 
- Multivalue answer policy => similar to simple routing, to return multiple values, but you have a healthcheck for each service, and we only return ip's that actually are healthy

## VPC

**What is a VPC**: A data center in the cloud, is where you deploy resources!

![](<../images/VPC diagram.png>)
- trafic comes from the internet gateway
- and goes to the router in the VPC
- router redirect to route tables
- route tables redirect it to network ACL => our first layer of defense -> you can block ip address  (Stateless)
- then security groups (Stateful)
- then we go to the subnet 

Default VPC:
- user friendly
- all subnets have a route out to internet
- EC2 instances have both public and private IP 

- private networks addreses not public to the internet
	- 10/8 -> 10.0.0.0 to 10.255.255.255
	- 172.16/12 -> 172.16.0.0. to 172.31.255.255
	- 192.168/16 -> 192.168.0.0 to 192.168.255.255

### VPC Peering 
- allow to connect VPC with another
-  even on differents aws accounts 
- and even  with other regions
- no transitive peering
- so if VPC a is connected to VPC B, and if VPC B is connected to VPC - C. VPC-A cannot be connected to VPC-C

### NAT instances & NAT Gateways
- allow subnets that are not in the public subnet -> to connect to the internet
- redundant inside the AZ
- after creating a NAT gateway into the public subnet => you need to update the routing table of the private subnet to route 0.0.0.0 to the nat-gateway

![](<../images/VPC - NAT GATEWAY.png>)

### Network Access control Lists (ACL)
- rules for allow deny trafic
- inbound / outbound
- PORT / IP range / PROTOCOL
- rules are in order

All VPC's have a default network ACL.
You need to associate subnets to network ACL, if a subnet is not associated with a 
network ACL, will use the default one
The default ACL is deny everything 👿
A subnet can have only one Network ACL, but a network ACL can be used by multiple subnets

### VPC Flow Logs
- allow to capture the logs of the firewall to cloudwatch logs or S3
- For the whole VPC, or the subnet, or an specific network interface

### Bastions
- is a computer with the minimum software installed that is public to the internet
- we have specific security group to use this computer to jump to a single computer in the private subnet

### VPC Endpoints
allows to connect to AWS services and VPC endpoint services (?) without going to the internet (no Internet Gateway, no NAT).

two types:
- interface endpoints 
- gateway endpoint  

### AWS Private Links
- connect services in one VPC to another VPC
- alternative you could use VPC peering => but would not scale for hundreds of VPC cause it's not transient

### AWS Transit Gateway
- simplify your network topology
- allow to peer with thousands of VPC and on-premise data centers

### AWS Network Costs
- traffic comming in into the VPC => FREE
- if subnet is talking to another subnet => free if in the same AZ
- if you go to another subnet in another AZ using internet is double expensive
- if you connect to another VPC in another region, is more expensive

## High Availability

### Elastic Load Balancer

3 typs of Load Balancers
- Application Load Balancer: Basically for webapps, work on layer 7. Are app aware (can look at cookies) 
- Networking Load Balancer: Work at layer 4 (TCP aware). More performance
- classic Load Balancer: legacy alb -> support for X-forwared and sticky session. you can do layer 4

Http 504 error => the ec2 behind a classic lb is not answering (timeout)

you can build a healthcheck on load balancer => check if a specific page is responding => if its unhealthy => ec2 instance will be mark as unhealthy

To configure ALB => first we create a Target group

### Sticky sessions
allow you to bind request of users to a specific EC2 instanse. so the EC2 instance get all the session requests

On ALB: sticky sessions work but they will be sent to Target group level rather than in a EC2 instance level

### What is Cross Zone Load Balancing

**Without cross zone**
Scenario: R53 is sending the traffic to 2 load balancers of two different regions. The region 1 => has 5 instances. Region 2 has 1 instance.  The region 2 instance, will receive 50% of the trafic, cause there is no more instances to balance

With cross zone... the LB can balance to instances in another region. and all instances will handle the same amount of balance

### Path Patterns
only for ALB. Redirect trafic from specific paths to different target groups => which means => different services

### AutoScaling

3 components
- Groups 
- Configuration templates -> launch template for EC2 instance (AMI, keypair, instance type, ...)
- Scaling options (rules of how to add, remove instances)
	- maintain current instance level at all times
	- scale manually
	- scale based on a schedule
	- scale based on demand (CPU threshold)
	- use predictive scaling


### HA architecture

