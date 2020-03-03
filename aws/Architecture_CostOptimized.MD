With AWS, you pay for Compute, storage, and data transfer

A cost optimized architecture involves the following
1. determine how to design cost optimized storage
2. determine how to design cost optimized compute

# Compute Cost
Compute Cost optimization can be achived by 
1. using Pay as you go
2. Pay less when you reserve
3. Pay even less per unit by using more

## Considerations for estimating the cost of using Amazon EC2
1. Clock hours of server time - 
2. Machine configurations - GPU instance can cost more than non-GPU
3. Machine purpose type - Reserved instances, on-demand, or spot instances - Reserved can be upto 75% cheaper than on-demand. Spot instances can be 30-45% cheaper than on-demand. Reserve instances are
    Standard RIs
    Convertible RIs - can be converted to other RIs
    Scheduled RIS - are reserved for specific times 
4. Number of instances
5. Load Balancing - 
6. Detailed monitoring - has cost
7. Auto scaling - can increase/decrease price
8. Elastic IP address - have a cost if not used
9. Operating Systems and software packages

## Cost saving Serverless architecture
Using AWS Lambda
Amazon S3
DynamoDB
Amazon API Gateway
CloudFront - can cache data. Can origin from S3, EC2, LB, HTTP server. No cost for data transfer between S3 and CF. 

## Considerations for estimating cost based on CloudFront
1. Traffic Distribution
2. Requests
3. Data Transfer out


# Storage Cost
## Considerations for S3 pricing are - 
Storage Class - 
    Standard - 
    Infrequent Access - 
    Glacier - 
Storage - 
Requests - 
Data transfer - 

## Considerations for EBS pricing are - 
Volumes - How many and what type of volumes
    SSD - higher iops, but costlier. random access
    HDD - lower iops, but cheaper. sequential access
IOPS - What type of iops
Snapshots - how frequently am I making snapshots and what is retention period. 
Data Transfer - 


# Test Axioms
If you know its going to be on, reserve it
Any unused CPU time is a waste of money
Use most cost effective data storage service and class
determine the most cost effective EC2 pricing model and instance type for each workload