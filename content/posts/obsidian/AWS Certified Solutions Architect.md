
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
- Encryption  in Transit (SSL/TLS)
- Encryption at rest (SSE -> Server Side Encryption)
	- S3 Managed keys - SSE-S3
	- AWS Key Management server - SSE-KMS
	- Server Side Encryption with Customer Provided Keys - SSE-C
- Client Side Encryption

### Lifecycle

- Transition current version of objects between storage classes
- transition previous version of objects between storage classes
- Expire current versions of objects
- permanently delete previous versions of objects

### Object Lock
WOTM (Write once, read many) => unmodifible and undeletable during a retention period

- Governance mode => some users can delete the files
- Compliance Mode => no user, even root user can overwrite or delete the file

### S3 Performance
- latency of around 100/200 ms first bites
- if you use SSE-KMS => limits of KMS quota
- Multipart uploads (mandatory for 5B files)
- Byte-Range fetches
	- Split the request into different offset 
- Requests
	-  5.500 GET/HEAD per sec per prefix
	- 3.500 PUT/COPY/POST/DELETE per sec per prefix
	- if you have files in different prefix's (folders) you can get better performance

### S3 Select
Pull information from S3 using SQL

Imagine you have CSV file in S3, and you need only some specific rows => instead of download the whole CSV => you ask S3 select to download a subset of the data you need

## 3. AWS Organization
Allow you to organize different AWS accounts into an organization that you created and centrally manager

Allow you to place policies to each OU (Organization Units) => that will go down to AWS Accounts

