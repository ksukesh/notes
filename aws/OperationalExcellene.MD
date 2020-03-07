Operation Excellence is the ability to run and monitor system to deliver business value and continually improve supporting processes and procedures
* Prepare
* Operate
* Evolve

Best practices

* perform operations with code
* Annotate documentation
* Make frequent, small, reversible changes - you need to have way to monitor your systems. After you make a change, you need to have way to monitor how your system behaves. 
* Refine Operations procedures frequently - constantly evolve 
* Anticipate failure
* Learn from all operational failures


Services supporting operational excellence
1. AWS Config - tracks resources such as EBS volumes and EC2 instances. It verifies that new resources comply with your configuration rules. 
2. AWS Cloud Formation - converts JSON and YAML in to infrastructure and resources
3. AWS Trusted Advisor - checks accounts for best practices for security, vulnerabilities, performance, cost  
4. AWS Inspector - checks EC2 instances for security vulnerabilities
5. VPC Flow logs - log network traffic. Capture level 3 and 4 level logs. 
6. AWS Cloud Trail - logs API calls. 
7. CloudWatch - logs metrics, and triggers alarms when metrics are exceeded. stores logs from EC2 instances, cloud trail, and lambda. It can also turn these logs in to metrics by extracting patterns from these log lines. 


# Test Axioms
* IAM Roles are easier and safer than keys and passwords
* Monitor metrics accross systems
* Automate responses to metrics where appropriate
* Provide alerts for anomalous conditions
