Three things to design secured architecture
1. Determine how to secure application tiers
2. Determine how to secure data
3. Determine the networking infrastructure for a single VPC application. 

# Securing Application Tier

Secure the infrastructure by using Shared Responsibility Model. Knowing what is customer vs AWS's responsibilities. 
Protect your AWS resources by Principle of Least privilege, and Identities. 

Identities in AWS
* IAM Users: Users created within the account
* Roles: Temporary identities used by EC2 instances, Lambdas, and external users
* Federation: Users with AD identities or other corporate credentials have roles assigned in IAM
* Web Identity Federation: Users with web identities from Amazon.com or other Open ID providers have roles assigned using Security Token Service (STS)

# Securing infrastucture

Compute Network architecture with security in mind
* Virtual Private Cloud (VPC)
    * Organize private IPs using Subnets
    * Secure the private network using Security Groups and Access Control list
    * Isolate the network using Internet Gateways/Virtual private gateawys/NAT Gateways -to control in and out of our vpcs
    * Control the traffic direction using Routes
* Design thinking of
* Security
* Routing
* Network Isolation
* Management
* Bastion Hosts

How to use Subnets - Use Subnets to define internet accessibility
Public Subnets
    To support inbound/outbound access to the public internet, include a routing table entry to an internet gateway
Private Subnets
    Do Not have a routing table entry to an internet gateway
    Not directly accessible from direct internet
    To support restricted, outbound only public internet access, typically use a jump box (NAT proxy/proxy/bastion host)

There are two ways of restricting or allowing access in a VPC
Security groups- operate at instance or the Network Interface level
Rules are explicit allow only
Are stateful - if a request comes in, it is allowed to get out
Supports VPC and EC2 Classic
Access Control lists - operate at the subnet level
Rules are allow and deny
Are stateless
Supports VPC only


You can seperate different tiers of an application using Security Groups. For example you can create Appliation tier security group and Database tier security group. 
Security groups can be configured to allow access from another security group. 

Both VPC and Security Groups are regional resources .

The services to get traffic in and out of the VPC 
Internet Gateway: Connect to the internet
Virtual Private Gateway: Connect to customer data center using VPN
AWS Direct Connect: Dedicated pipe using colo facilities
VPC Peering: Connect to other VPCs
NAT Gateways: Allow out going internet traffic from private subnets


Outbound traffic from private instance
NAT instance - Amazon EC2 instance as NAT in private subnet. Is not scalable
NAT Gateway - is AWS service and is highly scalable 


# Securing Data Tier
Data In Transit
* in and out of AWS
    * Use SSL over web
    * VPN for IPSec
    * IPSec over AWS Direct Connect
    * Import/Export/Snowball
* within AWS - data sent to AWS API 
    * AWS API calls are HTTPS by default
Data at rest
* Amazon S3 - Data stored is private by default, and requires AWS credentials to access
    * You can access over HTTP or HTTPS
    * There is an audit of all the access of objects
    * Supports ACL and policies
        * Buckets
        * Prefixes (director/folder)
        * Objects
* Amazon EBS

Data at rest can be encrypted using the following mechanisms
* Server Side encryption (SSE)
    * Amazon S3 Managed Keys (SSE-S3)
    * KMS Managed Keys (SSE-KMS)
    * Customer provided keys (SSE-C)
* Client Side Encryption (CSE)
    * KMS Managed Master encryption keys (CSE-KMS)
    * Customer managed Master encryption keys (CSE-C)

Keys can be managed using
* KMS
    * Customer software based key management
    * Integrated with many AWS services
    * Use directly from application
* AWS Cloud HSM
    * Hardware based Key management
    * Use directly from application
    * FIPS 140-2 compliant



Test Axioms
Lock down the root users
Security Groups only allow. NACLs allow explicit deny
Prefer IAM roles to access keys

