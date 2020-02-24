# FAQ
https://aws.amazon.com/ec2/faqs/
https://aws.amazon.com/storagegateway/faqs/
https://aws.amazon.com/athena/faqs/
https://aws.amazon.com/dynamodb/faqs/
https://aws.amazon.com/swf/faqs/

# Architecture
https://aws.amazon.com/architecture/well-architected/


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

Volumes and Snapshots
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

Encryption devices
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/building-shared-amis.html
https://aws.amazon.com/articles/public-ami-publishing-hardening-and-clean-up-requirements/
To Change the unencrypted disk to encrypted - Create Snapshot of the unencrypted volume -> Copy the snapshot, and while copying select encrypt the disk -> select a key -> Create an image (AMI) from encrypted volume -> Launch an instance with this new AMI. 

Snapshots of encrypted volumes are encrypted automatically. 
Volumes restored from encrypted snapshots are encrypted automatically
You can share snapshots, but only if they are unencrypted
These snapshots can be shared with other accounts or made public, if they are unencrypted
You can now encrypt the root device volumes upon creation of the EC2 instance. 


EBS Performance Optimization
There are a number of ways you can optimise performance above that of choosing the correct EBS type. One of the easiest options is to drive more I/O throughput than you can provision for a single EBS volume, by striping using RAID 0. You can join multiple gp2, io1, st1, or sc1 volumes together in a RAID 0 configuration to use the available bandwidth for these instances. You can also choose an EC2 instance type that supports EBS optimisation. This ensures that network traffic cannot contend with traffic between your instance and your EBS volumes. The final option is to manage your snapshot times, and this only applies to HDD based EBS volumes. When you create a snapshot of a Throughput Optimized HDD (st1) or Cold HDD (sc1) volume, performance may drop as far as the volume's baseline value while the snapshot is in progress. This behaviour is specific to these volume types. Therefore you should ensure that scheduled snapshots are carried at times of low usage. The one option on the list which is entirely incorrect is the option that states "Never use HDD volumes, always ensure that SSDs are used" as the question first states "In addition to choosing the correct EBS volume type for your specific task". HDDs may well be suitable to certain tasks and therefore they shouldn't be discounted because they may not have the highest specification on paper. 

Cloudwatch
Cloudwatch monitors performance. 
CLoudwatch is a monitoring service to monitor your AWS recources, as well as the applications that you run on AWS
it monitors performance. IT monitors - Compute, Storage and Content Delivery, 
On the EC2, it can monitor - CPU, network, Disk, Status Check. 
It monitors events every 5 minutes by default, but you can turn on the detailed monitoring to monitor every 1 minute. 
You can create CloudWatch alarm with trigger notifications

Cloud Trail
Is about auditing
increases the visibility into your user and resource activity by recording AWS management console actions and API calls. You can identify which users and accounts called the AWS, the IP address of the calls, and the time of the call. 

System Status Checks
This check verifies that your instance is reachable. We test that we are able to get network packets to your instance.
If this check fails, there may be an issue with the infrastructure hosting your instance (such as AWS power, networking or software systems). You may need to restart or replace the instance, wait for our systems to resolve the issue, or seek technical support.
This check does not validate that your operating system and applications are accepting traffic.

Instance Status Checks
This check verifies that your instance's operating system is accepting traffic.
If this check fails, you may need to reboot your instance or make modifications to your operating system configuration.


AWS CLI
You can use cli to do anything with AWS. 
You will need to setup access on IAM

IAM
You can create a new user from the IAM screen. YOu can have a user with Programmatic or the console access. You have to add the user to a group. THe group has the permission. You can download the access key of the user when you create it. If you loose the access key, you go to the user (Security Credentials), inactivate the current access key and then create a new access key. 

Roles
Roles are more secured than storing your access key on the VM. 
ROles are easier to manage
Roles can be assigned to EC2 instances after they are created by using both the console and the AWS cli
Roles are universal - you can use them in any region. 

User Data and Metadata
The following curl will give the user bootstrap
curl http://169.254.169.254/latest/user-data
The following will give the list of metadata that you can query on for an instance
curl http://169.254.169.254/latest/meta-data/
Once you type that, you can add a metadata name at the end to get the value. Like curl http://169.254.169.254/latest/meta-data/local-ipv4 will give the IP of the EC2 instance where we are running the curl from. 

Amazon Elastic File System (EFS)
is a file storage service for EC2. EFS provides quick way to create and manage File system quickly. The storage capacity is elastic, growing and shrinking automatically, when you add/remove files.
you pay for the storage that you use. There is no preprovisioning required. 
Can scale up to petabytes, and can support thousands of concurrent NFS connections
Data is stored across multiple AZ's within a region
Read after write consistency
Supports NFSv4 filesystem


EC2 Placement Group
Three types
Clustered - grouping of instances within a single AZ. Placement groups recommended for applications that need lower network latency, high network throughput or both. Only certain instances can be launched in to a Clustered Placement group. 
Spread - each instance placed on a different underlying hardware. Recommended for applications that have small number of critical instances that should be kept separate from each other.  Can provision across AZs
Partitioned - Multiple ec2 instances within the same partition. Amazon ensures taht each partition within a placement group has its own set of racks. Each rack has its own network and power source. No Two partitions within a placement group share the same racks, allowing you to isolate impact of hardware failure within your application. Can provision across AZs. Can be good for HDFS, HBase, and Cassandra.
Only certain types of instances can be launched in a placement group (Compute optimized, GPU, memory optimized, Storage Optimized)
AWS recommends homogeneous instances within Clustered placement groups. 
you can't merge placement groups. 
You can't move an existing instance into a placement group. Before you move the instance, the instance must be in a stopeed state. You can move or remove an instance using AWS SDK or CLI, but not using the COnsole. 

EC2 Summary
4 pricing models - On Demand (Pay by the hour), Reserved (contract for 1 to 3 years), Spot (bidding. for apps with flexible start and stop time), Dedicated hosts (physical dedicated servers for your use. Can be used for cases where you want to use existing software licenses)
Termination protection is turned off by default. 
On an EBS backed instance, the default for root EBS volume to be deleted when the instance is terminated. 
EBS Root volumes can be encrypted. You can also use a third party tool as Bit Locker to encrypt the root volume. THis can also be done while creating the AMIs in the console or using CLI or using API
All inbound traffic is blocked by default
All outbound traffic is allowed
Changes to security groups take effect immediately. 
You can have any number of EC2 instances within a SG. 
You can have multiple SGs attached to a EC2 instance. 
Security groups are stateful. If you open port 80, it will open for both inbound as well as outbound. 
Network ACLs are stateless. both inbound and outbound has to be opened separetely. 
you can't block specific IP address using SG, instead use NACL. In SG, you can add allow rules but not deny rules. 
EBS have SSDs and HDDs
SSD
Volume Types - General Purpose SSD (gp2|1GB-16TB|16000 Max IOPS), Provisioned IOPS SSD (io1|4GB-16TB|64000IOPS), 
HDD
Volume Types - Throughput Optimized HDD(st1|500GB-16TB|500), COld HDD(sc1|500GB-16TB|250), EBS Magnetic(Standard|1GB-1TB|40-200)
Volumes exist on EBS. Think of EBS as a virtual hard disk. 
Snapshots exists on S3. Snapshots are incremental. 

Storage Gateway
Storage Gateway allows hybrid storage between on-prem and AWS cloud. 


## Lambda
https://aws.amazon.com/blogs/compute/parallel-processing-in-python-with-aws-lambda/
https://aws.amazon.com/blogs/architecture/understanding-the-different-ways-to-invoke-lambda-functions/
https://aws.amazon.com/lambda/pricing/
https://docs.aws.amazon.com/lambda/latest/dg/lambda-permissions.html



# Database
https://aws.amazon.com/products/databases/
https://aws.amazon.com/nosql/key-value/

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


Troubleshooting
EC2 instance not connecting
https://aws.amazon.com/premiumsupport/knowledge-center/ec2-linux-ssh-troubleshooting/
We found that the VPC's route table was not configured with the correct internet gateway. We created an IG. Attached it to the VPC. Then changed the route table of VPC to have source as internet (0.0.0.0/0) and target as the IG. After all this, we created a EC2 instance. 
Wordpress wp-config.php not getting updated
Login to the instance, and create a new wp-config.php file. Add the content on the WP config page. 

Connecting to EC2 instance using putty
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html

No Default subnet - while creating EC2 instance
https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html#create-default-subnet

https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.html
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_CommonTasks.BackupRestore.html
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateSnapshot.html
https://aws.amazon.com/rds/faqs/#reserved-instances
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Storage.html#USER_PIOPS
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html
https://aws.amazon.com/rds/pricing/

## Dynamo DB
https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/CapacityUnitCalculations.html
https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html
https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadConsistency.html
https://aws.amazon.com/dynamodb/faqs/
https://aws.amazon.com/dynamodb/pricing/

## RedShift

## ElasticCache

## Athena
https://aws.amazon.com/athena/faqs/

# Security
## IAM
https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html
https://docs.aws.amazon.com/IAM/latest/UserGuide/resources.html

# Networking

## VPC
https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html
https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html


# Storage
https://help.acloud.guru/hc/en-us/articles/115002011194-AWS-Storage-Types-S3-EFS-EBS
https://d1.awsstatic.com/whitepapers/AWS%20Storage%20Services%20Whitepaper-v9.pdf?did=wp_card&trk=wp_card


## Storage Gateway
https://aws.amazon.com/storagegateway/faqs/

## EBS
https://aws.amazon.com/ebs/features/
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSPerformance.html


## EFS
https://docs.aws.amazon.com/efs/latest/ug/limits.html
https://aws.amazon.com/blogs/aws/new-infrequent-access-storage-class-for-amazon-elastic-file-system-efs/



# Other services
## Monitoring, Logging, Auditing, 
https://aws.amazon.com/xray/

## Simple Workflow service (SWF)
https://docs.aws.amazon.com/amazonswf/latest/developerguide/swf-welcome.html#http-service-apis
https://aws.amazon.com/swf/faqs/
