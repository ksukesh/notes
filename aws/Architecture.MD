https://aws.amazon.com/architecture/well-architected/

# Resilient Architecture

1. Choose resilient/reliable storage - so that data is not impacted in event of failure
2. Determine how to design decoupling mechanism using AWS services - to avoid impact on one component because of a failure in another. 
3. Determine how to design a multi-tier architecture solution - are decoupled. allows scaling up at a specific tier without needing to scale the whole application. 
4. Determine how to design HA and or FT solution - 


## Storage Solutions
* EC2 Instance Store - Generally used for caching or as a staging of data transfer
    * Ephemeral Volumes
    * Only certain EC2 instances have instance store
    * Fixed capacity
    * Disk types and capacity depends on Ec2 instance type
    * Application Level durability
* Elastic Block Store (EBS) - is attachable storage that connects to one EC2 instance at a time
    * Different types
    * Encryption
    * Snapshots
    * Provisioned Capacity for IOPS
    * Independent lifecyle than EC2 instance
    * Multiple volumes can be attached as RAID 0 and striped to create large volumes with higher throughput
    SSD (costiler) is good for random access and HDD (cheaper) for sequential option.  
* Elastic File System (EFS)
    * File storage on AWS 
    * Shared Storage 
    * Petabyte scale file system
    * Elastic Capacity
    * Supports NFS v4.0 and 4.1 protocol
    * Compatible with Linux-based AMI for EC2. Not for Windows
    EFS volumes can only attach to a single VPC at a time. Within this VPC, you find mount targets that your EC2 instances can connect to. 
* Amazon S3 - is a object store 
    * Consistency model - Strongly consistent for new objects and eventual consistency for updates (you may get older objects after updates). 
    * Storage Class and Durability - Standard(cheaper for reads and writes) and Standard IA(veery cheap for storage but expensive for writes)
    * Encryption (data at rest) - Server Side Encryption (SSE). SSE-S3 (AWS managed), SSE-KMS (Customer Managed), SSE-C (Customer Supplied)
    * Encryption (data in transit) - HTTPS
    * Versioning can be enabled
    * Access Control through IAM policies, through bucket policies, and through ACLs
    *  Multi-parts uploads
    * Internet API accessible
    * Virtually unlimited Capacity
    * Regional Availability
    * Highly durable (99.999999999%)    
* Amazon Glacier
    * Data backup and archive storage
    * Vaults and archives - archives are files, and vaults are collections of archives
    * Retrievals - expedited (expensive - can take upto 5 mins), standard (), bulk (cheapest - can take upto 12 hours for retrival)
    * Encryption
    * Amazon S3 object lifecycle policy can be setup to automatically move data to Glacier
    * Regionally available
    * Highly durable (99.999999999%)

## Decoupling Mechanism
Use of SQS queues/topics to decouple systems
Use of Load Balancers to decouple and balance load
Decouple IP address of server to the client - Use of Elastic IP address. It is static IP address that can move from one server to the other without changing. In the event of a new server coming up because of an error, the client does not need to change its URL. T

Fault Tolerance vs High Availability - FT is has a higher bar than HA. In case of FT, the user does not experience any degradation. This means that in case of FT, there should be another set of instances with same capacity ready to cater to the requests in case of a failure. 

## CloudFormation
Declarative programming language for deploying AWS resources
Uses templates and stacks to provision resources
    Templates are basic definitions of resources to create. Defined using JSON
    Stacks are collection of AWS resources
Create, update, and delete a set of resources as a single unit (stack)
If you plan to use CloudFOrmation to deploy EC2 instance in two different regions using same base AMI, you will have to use mappings to specify the base AMI since AMI IDs are different in each region.

# Compute - Lambda
A great way to make your application scale up and add resilience is to use Lambda. 
Lambda are fully managed compute service that runs stateless code (Node.js, Java, C#, Go and Python) in response to an event or on a time based interval
Allows you to run code without managing infrastructure like EC2 and auto-scaling groups


## 
RTO - Recovery time objective - How long does it take the system to recover and come back to service again. Measured in seconds, minutes, hours. 
RPO - How much data is lost when the system fails. It is measured in GB or MBs. It is also measured in units of time like minutes, hours. Meaning that we will loose data for that period of time. 


Test Axioms

* Expect Single AZ will never be the right answer. 
* Using AWS managed services should always be preffered
* FT and HA are not same thing
* expect that everything will fail at some time, and design accordingly

--------------


# Performant Architectures
1. choose performant storage and databases
2. Apply caching to improve performance
3. Design solutions for elasticity and scalability


## EBS 
|Volume Types|Max Volume Size|Max IOPS/volume|Max throughput volume|
|-----|-----|-----|-----|
|General Purpose SSDs|16TB|10K|160 MB/s|
|Provisioned SSDs|16TB|32K|500MB/s|More expensive than GP SSD
|Throughput Optimized HDDs|16TB|500|500MB/s|More expensive HDD option
|Cold HDDs|16TB|250|250MB/s|

## S3
Offload static content to S3 to improve Web Server's performance. 
To upload your data (photos, videos, documents), create a bucket in one of the regions, and upload any number of objects. 
Bucket URLs
Virtual hosted based urls, contains bucket name as the first part of the url
http://bucket.s3.amazonaws.com
http://bucket.s3-aws-region.amazonaws.com

Path style url contains bucket name and object as the path params. You can use region as part of the url or use without region, where aws will redirect to the specific region where the bucket is places. 
https://s3-ap-northeast-1.amazonaws.com/[bucketname]/[objectname]

Buckets are always tied to a region. 

Payment model
* Pay only for what you use
    * GBs per month
    * Transfer out of region
    * PUT, COPY, POST, LIST, and GET requests
* Free of charge
    * Transfer in to S3
    * Transfer in the same region
    * Transfer from s3 to CloudFront

Storage Classes
* General Purpose - AWS S3 standard
    * Higher availability requirements: Use cross-region replication
* Infrequent access data: Amazon S3 Standard - Infrequent Access
    * Lowest cost per GB stored
    * Higher cost per PUT, COPY, POST, or GET requests
    * 30-day storage minimum
Lifecycle policies can be used to move data over a period of time. A common pattern can be to 
move from S3 Standard to S3 Standard IA after 30 days
move from S3 standard IA to Amazon Glacier after 60 days
and delete from Glacier after 365 days. 

Important points 
S3 does not replicate data across regions. Its a regional service
Data stored on EBS is automatically store within an AZ

## Performant storage on DBs
### RDS
Use RDS
* Complex transactions or Complex queries
* A medium to high query/write rate
* No more than a single worker/shard
* High Durability

Do Not use RDS
* Massive read/write rates (example 150K writes/s)
* Sharding
* Simple GET/PUT requests and queries
* RDBMS customization

You can improve the performance of the RDS using read replicas. These can be used to offload the read requests to the read replicas. 
Microsoft SQL Servere and Oracle doesnt support read replication

### DynamoDB : Provisioned throughput
Is a non-relational database
Access patterns should certify the key-value pattern to use DynamoDB. Allocates resources based on throughput capacity requriements (read/write). It grows as the usage pattern changes. You will have to specify the throughput (how many reads/writes you want), and DynamoDB will scale up based on the throughput. The throughput is specified as RCU (read capacity unit) and WCU (Write capacity unit)
* Read Capacity Unit (for an input up to 4KB in size)
    * One strongly consistent read per second
    * or 2 eventual consistent read per second, if you can give up on strong consistency
* Write Capacity Unit (for an item up to 1 KB in size)
    * One write per second

### Redshift
is a relational database

## Caching

CloudFront - is useful for speeding up the content over the internet. It can be used as caching to serve Static or Dynamic content of the application. 
Caching can be applied to serve the static content using CloudFront (where it works as CDN). Once the user request comes, it tries to cater using the cache of CloudFront. It goes to S3 only if the content is not already present in the cache.
When used for dynamic content, the content is over the AWS backbone rather than public internet. 
You can setup the origin as S3 for static content. For dynamic content, the origin can be EC2 instances, ELB, or an HTTP server.
It improves service by using SSL, using AWS shield (to protect from DDos), using AWS WAF

*  Caching can also be done at application level using Elastic Cache. ElasticCache supports the following caching engines
    * Memcached - Simpler and easier to setup.
        * Multithreading
        * Low Maintenance
        * Easy horizontal scalability with auto discovery
    * Redis - more elaborate.
        * Support for Data Structures
        * Persistence
        * Atomic Operations
        * Pub/Sub messaging
        * Read replica/failover
        * Cluster Mode/Sharded Cluster


## Scaling
### Vertical Scaling
Is also called scaling up or scaling down, where we make the instance bigger or smaller. 

### Horizontal Scaling
IS also called scaling in or scaling out, where we increase or decrease the number of instances. 

### Auto scaling
Auto scaling can launch or terminate instances accross AZs. It can also automatically register instances with ELB. 
We manage the instances using CloudWatch. If there is an alarm, the auto scaling policies kick off and act on scaling needs. 
Auto scaling uses Launch Configuration as a template to launch a fully configured instance
Auto scaling can be also scheduled based on known usage pattern and the time taken to scale up the instances. If it takes 20 mins to add instance, schedule at least 20 mins before the load is expected to come. 

Auto scaling components
* Autoscaling launch configuration 
    * specifies EC2 instance size and AMI name. 
* Auto scaling group 
    * references the launch configuration
    * specifies min, max, and desired size of the auto scaling group
    * May reference an ELB
    * Health check type
* Auto scaling policy
    * specifies how much to scale in or out
    * one or more may be attached to auto scaling group. 
Autoscaling uses CloudWatch to know when to change the scale
CloudWatch can monitor CPU, Network, and Queue Size.
It is important to understand CloudWatch logs, and difference between custom and default metrics. 

Load Balancer balances the instances


Text Axioms
