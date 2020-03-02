# FAQ
https://aws.amazon.com/ec2/faqs/
https://aws.amazon.com/lambda/faqs/
https://aws.amazon.com/elasticloadbalancing/faqs/
https://aws.amazon.com/ec2/autoscaling/faqs/
https://aws.amazon.com/ebs/faqs/
https://aws.amazon.com/ebs/faqs/
https://aws.amazon.com/storagegateway/faqs/
https://aws.amazon.com/efs/faq/
https://aws.amazon.com/rds/aurora/faqs/
https://aws.amazon.com/dynamodb/faqs/
https://aws.amazon.com/elasticache/faqs/
https://aws.amazon.com/vpc/faqs/
https://aws.amazon.com/route53/faqs/
https://aws.amazon.com/iam/faqs/
https://aws.amazon.com/cloudwatch/faqs/
https://aws.amazon.com/cloudtrail/faqs/
https://aws.amazon.com/kinesis/data-streams/faqs/
https://aws.amazon.com/cloudfront/faqs/
https://aws.amazon.com/sqs/faqs/
https://aws.amazon.com/sns/faqs/
https://aws.amazon.com/cloudformation/faqs/
https://aws.amazon.com/amazon-mq/faqs/
https://aws.amazon.com/ram/faqs/
https://aws.amazon.com/athena/faqs/
https://aws.amazon.com/swf/faqs/

# Cheatsheets
https://tutorialsdojo.com/aws-cheat-sheet-aws-certified-solutions-architect-associate/
https://tutorialsdojo.com/comparison-of-aws-services-for-udemy-students/

https://tutorialsdojo.com/aws-cheat-sheet-amazon-cloudfront/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-api-gateway/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-elastic-compute-cloud-amazon-ec2/
https://tutorialsdojo.com/aws-cheat-sheet-aws-lambda/
https://tutorialsdojo.com/aws-cheat-sheet-aws-systems-manager/
https://tutorialsdojo.com/aws-cheat-sheet-aws-identity-and-access-management-iam/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-s3/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-elastic-container-service-amazon-ecs/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-ebs/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-elasticache/
https://tutorialsdojo.com/aws-cheat-sheet-redis-cluster-mode-enabled-vs-disabled-vs-memcached/
https://tutorialsdojo.com/amazon-aurora/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-dynamodb/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-redshift/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-relational-database-service-amazon-rds/
https://tutorialsdojo.com/aws-cheat-sheet-cloudwatch-agent-vs-ssm-agent-vs-custom-daemon-scripts/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-cloudwatch/
https://tutorialsdojo.com/aws-cheat-sheet-aws-key-management-service-aws-kms/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-vpc/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-elasticsearch-amazon-es/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-kinesis/
https://tutorialsdojo.com/aws-cheat-sheet-aws-directory-service/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-efs/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-s3-vs-ebs-vs-efs/
https://tutorialsdojo.com/aws-cheat-sheet-aws-cloudtrail/


https://tutorialsdojo.com/aws-cheat-sheet-aws-auto-scaling/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-mq/
https://tutorialsdojo.com/aws-cheat-sheet-amazon-sqs/



# Comparisions
https://tutorialsdojo.com/comparison-of-aws-services/
https://tutorialsdojo.com/amazon-s3-vs-ebs-vs-efs/


# Usefuls
Locality of services/resources - https://jayendrapatil.com/aws-global-vs-regional-vs-az-resources/

# White papers
https://d1.awsstatic.com/whitepapers/aws-overview.pdf
https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf
https://d1.awsstatic.com/whitepapers/AWS_Cloud_Best_Practices.pdf
https://d1.awsstatic.com/whitepapers/Security/AWS_Security_Best_Practices.pdf
https://d1.awsstatic.com/whitepapers/AWS%20Storage%20Services%20Whitepaper-v9.pdf
https://d1.awsstatic.com/whitepapers/aws-building-fault-tolerant-applications.pdf



# Architecture
https://aws.amazon.com/architecture/well-architected/

- - - - 

# Compute

## EC2
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/terminating-instances.html#delete-on-termination-running-instance
https://aws.amazon.com/blogs/security/how-to-protect-data-at-rest-with-amazon-ec2-instance-store-encryption/
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html
https://aws.amazon.com/ec2/faqs/
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ri-market-general.html
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ri-modifying.html
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html
https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-instances.html
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html
https://aws.amazon.com/blogs/security/easily-replace-or-attach-an-iam-role-to-an-existing-ec2-instance-by-using-the-ec2-console/
https://aws.amazon.com/blogs/security/new-attach-an-aws-iam-role-to-an-existing-amazon-ec2-instance-by-using-the-aws-cli/

### EBS - Volumes and Snapshots
Volumes Exists on EBS. Think of EBS as a virtual disk. 
Snapshots exists on S3. 
Snapshots are point in time copies of the volumes.
Snapshots are incremental - this means that only the block that has changed gets copied to S3. 
If its the first snapshot, it may take some time to create. 
Its best practice (but not required) to stop the instance before taking the snapshot from its root EBS volume. 
You can create AMIs from snapshots. 
You can change the EBS volume size and type on the fly
Volumes will be in same AZ as the instance. 
To migrate an instance from one AZ to other, create a snapshot of the volume -> create AMI from it -> Create the instance using the AMI in another AZ. 
To migrate an instance from one region to the other, Create a snapshot of the volume -> create an AMI from it -> Copy the AMI from one region to the other -> Create instance using the AMI in new region. 

Instance Store VOlumes are called Ephemeral storage. 
Instance Store volumes can't be stopped. If the instance fails, the data will be lost. 
EBS backed instances can be stopped without losing the data. 
By default, both ROOT volumes will be deleted on termination. However, with EBS volumes, you can tell AWS to keep the device volume. 

#### Encryption devices
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/building-shared-amis.html
https://aws.amazon.com/articles/public-ami-publishing-hardening-and-clean-up-requirements/
To Change the unencrypted disk to encrypted - Create Snapshot of the unencrypted volume -> Copy the snapshot, and while copying select encrypt the disk -> select a key -> Create an image (AMI) from encrypted volume -> Launch an instance with this new AMI. 

Snapshots of encrypted volumes are encrypted automatically. 
Volumes restored from encrypted snapshots are encrypted automatically
You can share snapshots, but only if they are unencrypted
These snapshots can be shared with other accounts or made public, if they are unencrypted
You can now encrypt the root device volumes upon creation of the EC2 instance. 


#### EBS Performance Optimization
There are a number of ways you can optimise performance above that of choosing the correct EBS type. One of the easiest options is to drive more I/O throughput than you can provision for a single EBS volume, by striping using RAID 0. You can join multiple gp2, io1, st1, or sc1 volumes together in a RAID 0 configuration to use the available bandwidth for these instances. You can also choose an EC2 instance type that supports EBS optimisation. This ensures that network traffic cannot contend with traffic between your instance and your EBS volumes. The final option is to manage your snapshot times, and this only applies to HDD based EBS volumes. When you create a snapshot of a Throughput Optimized HDD (st1) or Cold HDD (sc1) volume, performance may drop as far as the volume's baseline value while the snapshot is in progress. This behaviour is specific to these volume types. Therefore you should ensure that scheduled snapshots are carried at times of low usage. The one option on the list which is entirely incorrect is the option that states "Never use HDD volumes, always ensure that SSDs are used" as the question first states "In addition to choosing the correct EBS volume type for your specific task". HDDs may well be suitable to certain tasks and therefore they shouldn't be discounted because they may not have the highest specification on paper. 


#### System Status Checks
This check verifies that your instance is reachable. We test that we are able to get network packets to your instance.
If this check fails, there may be an issue with the infrastructure hosting your instance (such as AWS power, networking or software systems). You may need to restart or replace the instance, wait for our systems to resolve the issue, or seek technical support.
This check does not validate that your operating system and applications are accepting traffic.

#### Instance Status Checks
This check verifies that your instance's operating system is accepting traffic.
If this check fails, you may need to reboot your instance or make modifications to your operating system configuration.


#### AWS CLI
You can use cli to do anything with AWS. 
You will need to setup access on IAM

#### IAM
You can create a new user from the IAM screen. YOu can have a user with Programmatic or the console access. You have to add the user to a group. THe group has the permission. You can download the access key of the user when you create it. If you loose the access key, you go to the user (Security Credentials), inactivate the current access key and then create a new access key. 

#### Roles
Roles are more secured than storing your access key on the VM. 
ROles are easier to manage
Roles can be assigned to EC2 instances after they are created by using both the console and the AWS cli
Roles are universal - you can use them in any region. 

#### User Data and Metadata
The following curl will give the user bootstrap
curl http://169.254.169.254/latest/user-data
The following will give the list of metadata that you can query on for an instance
curl http://169.254.169.254/latest/meta-data/
Once you type that, you can add a metadata name at the end to get the value. Like curl http://169.254.169.254/latest/meta-data/local-ipv4 will give the IP of the EC2 instance where we are running the curl from. 




### EC2 Placement Group
Three types
1. Clustered - grouping of instances within a single AZ. Placement groups recommended for applications that need lower network latency, high network throughput or both. Only certain instances can be launched in to a Clustered Placement group. 
2. Spread - each instance placed on a different underlying hardware. Recommended for applications that have small number of critical instances that should be kept separate from each other.  Can provision across AZs
3. Partitioned - Multiple ec2 instances within the same partition. Amazon ensures taht each partition within a placement group has its own set of racks. Each rack has its own network and power source. No Two partitions within a placement group share the same racks, allowing you to isolate impact of hardware failure within your application. Can provision across AZs. Can be good for HDFS, HBase, and Cassandra.

Only certain types of instances can be launched in a placement group (Compute optimized, GPU, memory optimized, Storage Optimized)
AWS recommends homogeneous instances within Clustered placement groups. 
you can't merge placement groups. 
You can't move an existing instance into a placement group. Before you move the instance, the instance must be in a stopeed state. You can move or remove an instance using AWS SDK or CLI, but not using the COnsole. 

### EC2 Summary
* 4 pricing models - On Demand (Pay by the hour), Reserved (contract for 1 to 3 years), Spot (bidding. for apps with flexible start and stop time), Dedicated hosts (physical dedicated servers for your use. Can be used for cases where you want to use existing software licenses)
* Termination protection is turned off by default. 
* On an EBS backed instance, the default for root EBS volume to be deleted when the instance is terminated. 
* EBS Root volumes can be encrypted. You can also use a third party tool as Bit Locker to encrypt the root volume. THis can also be done while creating the AMIs in the console or using CLI or using API
* All inbound traffic is blocked by default
* All outbound traffic is allowed
* Changes to security groups take effect immediately. 
* You can have any number of EC2 instances within a SG. 
* You can have multiple SGs attached to a EC2 instance. 
* Security groups are stateful. If you open port 80, it will open for both inbound as well as outbound. 
* Network ACLs are stateless. both inbound and outbound has to be opened separetely. 
you can't block specific IP address using SG, instead use NACL. In SG, you can add allow rules but not deny rules. 
* EBS have SSDs and HDDs
    * Volume Types - General Purpose SSD (gp2|1GB-16TB|16000 Max IOPS), Provisioned IOPS SSD (io1|4GB-16TB|64000IOPS), 
    * Volume Types - Throughput Optimized HDD(st1|500GB-16TB|500), COld HDD(sc1|500GB-16TB|250), EBS Magnetic(Standard|1GB-1TB|40-200)
* Volumes exist on EBS. Think of EBS as a virtual hard disk. 
* Snapshots exists on S3. Snapshots are incremental. 



## Load Balancers
https://docs.aws.amazon.com/AmazonECS/latest/developerguide/load-balancer-types.html
ELBs can be found in EC2 section of the Menu. Dont look for them in network section.  

There are three types
1. Application LB - suited for load balancing of http and https traffic. They operate at layer 7 of tcp and are application aware. They are intelligent and you can create advanced request routing for sending specific requests to specific servers. Can be internal or internet-facing. 
2. Network LB
suited for TCP traffic where extreme performance is required. Operates at layer 4 of tcp. Capable of handling millions of requests per second with ultra low latency. 
3. Classic LB - can be used for http/https lb on layer 7 specific features like sticky sessions and x-forward. You can also use for tcp lb on layer 4. Can be internal(within VPC with internal ip) of external (internt facing) 
    Classic LB responds with 504 (Gateway timeout) if your application stops responding.

x-forwarded-for header - with LB in between the application and the client, the client ip that reaches to the application is the LB IP. TO get the actual ip of the client, use x-forwarded-for header from the request.  

Instances monitored by ELB are reported as InService or OutofService. 
Health checks can be configured while creating the LB. To configure health check, http url can be mentioned. 
LB has their own DNS name, and not the IP address. 

To create Application LB, first create Target group, which is a group of EC2 instances, IP addresses, or Lambda functions.
LB routes requests to the targets in a target group using the target group settings that you specify, and performs health checks on the targets using the health check settings that you specify.

Sticky Sessions allows to bind user sessions to a specific EC2 instance. 
Classic load balancers can use sticky sessions to route user specific request to the specific instance. 
Application load balancers can use sticky sessions to route user specific request to the target group and not individual instance. 

Cross Zone LB
If you dont have cross zone lb enabled, the load on one zone can be more than the other, based on the number of instances in each zone. 
If you ahve cross zone lb enabled, the load on all ec2 instances will be equally distributed because lb can go across zone to cater to requets 

Path patterns allow you to direct traffic based on URL in the request. 

## Autoscaling groups
To configure the autoscaling group. First, create/choose either a launch configuration or a launch template(new) to specify the parameters that your Auto Scaling group uses to launch instances. Using these, the autoscaled instance will be created. 
Launch Configuration is the template for the type of intances for which auto scaling has to be configured.
Launch Template gives you iption to launch one type of instane or a combination of instance types and purchase options.  

Then define the autoscaling group, by selecting the launch configuration, network, sub-network, number to start with, set scaling policy [ based on cpu, network load, request count]. You can also add notification 

https://aws.amazon.com/blogs/aws/new-ec2-auto-scaling-groups-with-multiple-instance-types-purchase-options/?&trk=ha_a131L000005uJTZQA2&trkCampaign=pac-edm-2019-spot-sitemerch-autoscalingblog&sc_ichannel=ha&sc_icampaign=Adoption_Campaign_pac-edm-2019-spot-site_merch-adoption-all-auto_scaling_console_test&sc_ioutcome=Enterprise_Digital_Marketing


## Lambda
https://aws.amazon.com/blogs/compute/parallel-processing-in-python-with-aws-lambda/
https://aws.amazon.com/blogs/architecture/understanding-the-different-ways-to-invoke-lambda-functions/
https://aws.amazon.com/lambda/pricing/
https://docs.aws.amazon.com/lambda/latest/dg/lambda-permissions.html

- - - - 

# Storage

https://aws.amazon.com/products/databases/
https://aws.amazon.com/nosql/key-value/

## S3

## Amazon Elastic File System (EFS)
is a file storage service for EC2. EFS provides quick way to create and manage File system quickly. The storage capacity is elastic, growing and shrinking automatically, when you add/remove files.
you pay for the storage that you use. There is no preprovisioning required. 
Can scale up to petabytes, and can support thousands of concurrent NFS connections
Data is stored across multiple AZ's within a region
Read after write consistency
Supports NFSv4 filesystem

## Storage Gateway
Storage Gateway allows hybrid storage between on-prem and AWS cloud. 


## RDS
RDS runs on VMs, but you can't access them. You can't patch them either. 
RDS is not serverless, except serverless Aurora


sukeshtest.c3fhzsejf0ax.us-east-1.rds.amazonaws.com
In the exercise, we created a RDS instance. It needs 2 subnets in 2 different AZs to create.
We created RDS in a different security group to protect it, and then gave access to the web security group in the rds sg. 
    We gave access by adding the inbound rule of rds-sg for type MySql/Aurora, with source being the web sg. 
While creating the rds instance, we made sure that we create the db as well. 
We then created a wordpress site to access the db. The wordpress site running on the EC2 instanece. We installed the wordpress site using the startup script. 
Once our instance was created, we went to the public ip of the instance, which asked us to configure the RDS details. 

### RDS Backups
Automated Backups
Automated backups allow you to recover your database in a retention period of 1 to 35 days. Automated backups take a full daily snapshots, and also store the full transaction logs throughout the day. When you do a recovery, AWS will first take the most recent daily backup, and then apply the transaction logs relevant to that day. THis allows a point in time recovery down to a second.
Automated backups, enabled by default, stores the backup data in S3, and you get free storage equal to the size of your database. During the backup window, there may be elevated latency. 

### Database Snapshots
Are manual backups, and are kept even after delete of the db instance (unlike automated).

The restoration happens in a new RDS instance with a new DNS name (and not the original one)

### Encryption at Rest
Available for Oracle, MySql, SqlServer, PostgreSql, MariaDB, and Aurora. Supported using AWS KMS. Once the RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas, and snapshots. 

### Multi AZ
Keeps a copy of the prod database to another AZ, which acts as a failover. This is not used for performance improvements. 
Available for Oracle, MySql, SqlServer, PostgreSql, and MariaDB.

### Read Replica
Asynchronous replication of the DB for read heavy workloads. 
Each replica has its own DNS endpoint. You can have replicas that have multi-az. You can also create the replicas of multi-az dbs. 
Read replicas can be promoted to their own database, at which point the replication stops. 
You can have read replica in a second region. 
Available for Oracle, MySql, SqlServer, PostgreSql, MariaDB, and Aurora.



### References - RDS
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.html
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_CommonTasks.BackupRestore.html
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateSnapshot.html
https://aws.amazon.com/rds/faqs/#reserved-instances
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Storage.html#USER_PIOPS
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html
https://aws.amazon.com/rds/pricing/

## Dynamo DB
is a nosql db, with single digit millisecond latency at any scale. it is a fully managed document or key-value data store. 
Its flexible data model and reliable performance makes it a great fit for mobile, web, gaming, ad-tech, iot kind of apps.  
stored on ssd storage. spread across 3 different data centers. default is eventual consistent reads (with almost 1 second delay). you can enable strongly consistent reads if your application needs to read right after (or if 1 second is unacceptable) the read. 

### References - Dynamo DB
https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/CapacityUnitCalculations.html
https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html
https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadConsistency.html
https://aws.amazon.com/dynamodb/faqs/
https://aws.amazon.com/dynamodb/pricing/

## RedShift

### References - RedShift

## ElastiCache
https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/WhatIs.html

### References - 

## Athena
https://aws.amazon.com/athena/faqs/

### References - 

# Security
## IAM
https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html
https://docs.aws.amazon.com/IAM/latest/UserGuide/resources.html
### References - 

# Networking

## VPC

### References - 
https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html
https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html

https://docs.aws.amazon.com/vpc/latest/userguide/security.html

## Route53
Elastic Load Balancers dont have pre-defined IPv4 addresses; you resolve to them using a DNS name
TODO - Understand diffrence between Alias Record and CNAME
Given a choice, always choose an Alias Record over cname. 

Common DNS Types
1. SOA Records
2. NS Records
3. A Records
4. CNAME
5. MX Records
6. PTR Records

*** It can take up to 3 days to register the domain name. ***

### Routing Policies
1. Simple Routing - You have one record in DNS with multiple IP addresses. If you have multiple IPs in a record, Route53 returns all the values in a random order
2. Weighted Routing - You have one IP address per record. Each record is assigned a weight. The weights togther add up t 100. Health Checks are way to setup check health checks on individual records. If a record fails a health check, it is removed from R53, until it passes the health check. You can add SNS notification for a HC failure. 
3. Latency based Routing - Allows to route your traffic based on the lowest network latency for your end user (ie which region will give them the fastest response time). To use Latency based routing, you create a latency resource record set for EC2 (or ELB) resource in each region that hosts your website. when Route 53 receives a query for your website, it selects the latency resource record set for the region that gives the user the lowest latency.   
4. Failover Routing - used when you want to create active passive setup 
5. Geolocation Routing - Geolocation Routing lets you choose where your traffic will be sent based on the geographic location of your users 
6. Geoproximity Routing - routes traffic to your website based on the georgraphic location of hte user and your resource. You can choose to route more or less traffic of a given resource by speficying a value to a given resource, known as bias. A bias shrinks or expands the size of the geo region from which the traffic is routed to a resource. To use geo proximity routing, you must use Route 53 traffic flow 
7. Multivalue Answer Routing - lets you configure R53 to return multiple values, such as IP addresses for your web servers, in response to DNS query. You can specify multiple values for almost any record, but multi value answer routing also lets you check the health of each resource, so R53 return values for only healthy resources. This is "similar" to simple routing. 

### References - Route53
https://aws.amazon.com/route53/faqs/

## Security Group
A security group acts as a virtual firewall for your instance to control inbound and outbound traffic. When you launch an instance in a VPC, you can assign up to five security groups to the instance. Security groups act at the instance level, not the subnet level. Therefore, each instance in a subnet in your VPC could be assigned to a different set of security groups. If you don't specify a particular group at launch time, the instance is automatically assigned to the default security group for the VPC.

### References - Security Group
https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html


# Storage

https://help.acloud.guru/hc/en-us/articles/115002011194-AWS-Storage-Types-S3-EFS-EBS
https://d1.awsstatic.com/whitepapers/AWS%20Storage%20Services%20Whitepaper-v9.pdf?did=wp_card&trk=wp_card


## Storage Gateway

### References - Storage Gateway
https://aws.amazon.com/storagegateway/faqs/

## EBS
https://aws.amazon.com/ebs/features/
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSPerformance.html
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html

### References - EBS

## EFS
https://docs.aws.amazon.com/efs/latest/ug/limits.html
https://aws.amazon.com/blogs/aws/new-infrequent-access-storage-class-for-amazon-elastic-file-system-efs/


### References - EFS

# Other services
## Monitoring, Logging, Auditing, 
https://aws.amazon.com/xray/

### CloudWatch
Amazon RDS provides metrics in real time for the operating system (OS) that your DB instance runs on. You can view the metrics for your DB instance using the console, or consume the Enhanced Monitoring JSON output from CloudWatch Logs in a monitoring system of your choice. By default, Enhanced Monitoring metrics are stored in the CloudWatch Logs for 30 days. To modify the amount of time the metrics are stored in the CloudWatch Logs, change the retention for the RDSOSMetrics log group in the CloudWatch console.

Take note that there are certain differences between CloudWatch and Enhanced Monitoring Metrics. CloudWatch gathers metrics about CPU utilization from the hypervisor for a DB instance, and Enhanced Monitoring gathers its metrics from an agent on the instance. As a result, you might find differences between the measurements, because the hypervisor layer performs a small amount of work. Hence, enabling Enhanced Monitoring in RDS is the correct answer in this specific scenario.
Cloudwatch
Cloudwatch monitors performance. 
CLoudwatch is a monitoring service to monitor your AWS recources, as well as the applications that you run on AWS
it monitors performance. IT monitors - Compute, Storage and Content Delivery, 
On the EC2, it can monitor - CPU, network, Disk, Status Check. 
It monitors events every 5 minutes by default, but you can turn on the detailed monitoring to monitor every 1 minute. 
You can create CloudWatch alarm with trigger notifications

CloudWatch has available Amazon EC2 Metrics for you to use for monitoring CPU utilization, Network utilization, Disk performance, and Disk Reads/Writes. In case that you need to monitor the below items, you need to prepare a custom metric using a Perl or other shell script, as there are no ready to use metrics for these:
1. Memory utilization
2. disk swap utilization
3. disk space utilization
4. page file utilization
5. log collection

Take note that there is a multi-platform CloudWatch agent which can be installed on both Linux and Windows-based instances. You can use a single agent to collect both system metrics and log files from Amazon EC2 instances and on-premises servers. This agent supports both Windows Server and Linux and enables you to select the metrics to be collected, including sub-resource metrics such as per-CPU core. It is recommended that you use the new agent instead of the older monitoring scripts to collect metrics and logs.

### CloudTrail

Is about auditing
increases the visibility into your user and resource activity by recording AWS management console actions and API calls. You can identify which users and accounts called the AWS, the IP address of the calls, and the time of the call. 

### Resource Access Manager (RAM)
AWS Resource Access Manager (RAM) is a service that enables you to easily and securely share AWS resources with any AWS account or within your AWS Organization. You can share AWS Transit Gateways, Subnets, AWS License Manager configurations, and Amazon Route 53 Resolver rules resources with RAM.
Many organizations use multiple accounts to create administrative or billing isolation, and to limit the impact of errors. RAM eliminates the need to create duplicate resources in multiple accounts, reducing the operational overhead of managing those resources in every single account you own. You can create resources centrally in a multi-account environment, and use RAM to share those resources across accounts in three simple steps: create a Resource Share, specify resources, and specify accounts. RAM is available to you at no additional charge.

https://aws.amazon.com/ram/

## Simple Workflow service (SWF)
https://docs.aws.amazon.com/amazonswf/latest/developerguide/swf-welcome.html#http-service-apis
https://aws.amazon.com/swf/faqs/





# Troubleshooting
EC2 instance not connecting
https://aws.amazon.com/premiumsupport/knowledge-center/ec2-linux-ssh-troubleshooting/
We found that the VPC's route table was not configured with the correct internet gateway. We created an IG. Attached it to the VPC. Then changed the route table of VPC to have source as internet (0.0.0.0/0) and target as the IG. After all this, we created a EC2 instance. 
Wordpress wp-config.php not getting updated
Login to the instance, and create a new wp-config.php file. Add the content on the WP config page. 


Connecting to EC2 instance using putty
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html

No Default subnet - while creating EC2 instance - aws ec2 create-default-subnet --availability-zone us-east-1a
https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html#create-default-subnet

NO Public IP for the EC2 instance. 
You may have used non-default subnet, and have selected Auto Assign Setting as disabled while creating the instance. Change the Auto Assign to Enable



1. 