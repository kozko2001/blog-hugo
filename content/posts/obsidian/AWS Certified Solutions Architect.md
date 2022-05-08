
---
title: AWS certified solution architect associate
date: 2022-05-08 00:00:00
---
---
# AWS certified solution architect associate
- **Region**: is a geographical zone that have a at least two AZ who are autonomous from each other.
- **AZ (Availability Zones)**: a datacenter, in a region, with all that needs to be able to run the services
- **Edge locations**: small servers all around the world, that serve content from CloudFront for geo caching.

## 1 IAM

- Users: A user, they will not have access to the console if we don't check the option
- Groups: group of user that inherit the policies of the group
- Roles: services in AWS can have roles, that have policies allowing to access to some services
- Policies: actual permissions allowing or denying access to a resource

## 2. S3

- Files can have upto 5Tb
- universal namespace -> bucket names have to be unique -> url 
- Objects
	- Key => filename
	- Value => content of the file
	- Version ID =>
- You can protect S3 files => making MFA need for delete files

### Guarentees
- Build for 99.99% availability
- Amazon guarantees 99.9 aailability
- amazon guarantees 11 9's durability

### Consistency
- Read after write for PUTS of new Objects
- Eventual consistency (secs) for overwrites and deletes

### Storages Classes
- S3 Standar 99.99 availbility - 11 9's durability
- S3 - IA (Infrequently accessed) - instant access but rapid access => low fees but charged a retrieval fee
- S3 One Zone - IA =>
- S3 - Intelligent tiering => ML moving the tiers depending how much you use
- Glacier => takes minutes/hours to retrieve the object
- Glacier Deep Archive => 12 hours 

### Costs
- Storage
- num of request Request 
- depending on the tier
- Data transfer
- Transfer acceleration
- Cross region replication => use edge location  and use amazon backbone network

### Security
- Bucket policies
- Access Control Lists (policies inside the S3)

### Encryption
- Encryption  in Transit (https)