# **AWS Interview Questions**
## DAY1
### 1. What is Amazon EC2:
          Amazon Elastic compute cloud provides on-demand capacity in AWS cloud. It allows users to launch virtual machines(instances) on demand and scale them up and down as needed.
### 2. What are the different types of EC2 Instances:
          EC2 instances are categoized as 
              1) General Purpose 2) Compute Optimized 3) Memory Optimized 4) Storage Optimized 5) Accelerated Computing
### 3. What are the differences between On-Demand, Reserved and Spot Instances:
          On-Demand: Pay per sec/min, no commitment. Best used for short term or unpredictable workloads
          Reserved: 1-3 yr commitment, upto 75% cheaper than on-demand. Best used for long term and steady workloads
          Spot-instances: upto 90% cheaper but can be terminated by AWS. Best used for fault tolerant workloads.
### 4. What are key-components of an EC2 instance:
          Ami, Instance Type, Security Groups, key-pairs, EBS volumes, Elastic IP.
### 5. What is AMI:
          Amazon machine image is a preconfigured template that includes OS, Application server, custom software
### 6. Difference between EBS(Elastic block storage) and instance store:
          EBS are persistent storage (data persists after instance stops whereas data is lost when instance stops in instance store.
### 7. What is an Elastic IP:
          An elastic ip is static, public IP address that remains the same even if an instance is stopped or restarted.
### 8. How do you scale EC2 instances:
          Two types of scaling: Vertical and horizontal. Vertical scaling is when you increase CPU/RAM. Horizontal scaling is to add more instances using auto scaling groups.
### 9. What are security groups and how do they work:
          Security groups act as firewall that control inbound and outbound traffic for EC2 instance
### 10. How does EC2 instance handle failures:
          -> If an instance fails, AWS automatically replaces it using Auto scaling Groups.
          -> Use Elastic Load balancer to distribute traffic and avoid single point of failure.
          -> Enable cloudwatch alarms for proactive monitoring
## DAY2
### 11. What is the difference between stop, terminate and reboot in EC2:
          -> Stop: Halts the instance but keeps the storage (EBS persists)
          -> Terminate: Deletes the instance and its storage (unless set to 'keep')
          -> Reboot: Restarts the instance without data loss
### 12. How does EC2 integrate with Auto Scaling and Load Balancer:
          Auto scaling group (ASG): Automatically adds/removes instances based on demand
          Elastic Load Balancer (ELB): Distributes traffic among instances for high availability
### 13. What are placement groups and when should you use them:
          Placement groups control instance placement for performance. Depending on type of workload, you can use following placement strategies.
          -> Cluster placement group: Low latency network 
          -> Spread placement groups: High availability
          -> Partition placement groups: Used in large scale distribed systems
### 14. How do you secure and EC2 instance:
          -> You can use IAM roles instead of credentials
          -> By enabling Security groups and Network ACLs
          -> Regularly patch and update instances
          -> Restrict SSH access with key pairs and specific IPs
### 15. What is EC2 Hibernate State, and how does it work:
          Hibernation saves RAM contents to EBS Storage and restores them when the instance restarts. If you pause a large application, hibernation resumes it without reloading data.
### 16. How do you troubleshoot high CPU usage in EC2:
          Use CloudWatch Metrics to monitor CPU utilization
          Check running processes(top cmd)
          Optimize application code or upgrade instance type
### 17. What is the difference between EC2 and lambda:
          EC2 and Aws Lambda are compute services. 
          EC2: 
              Type: Virtual Machines (Instances)
              Management: Manage OS, scaling and maintenance
              Scaling: Manual or Auto Scaling
              Pricing: Pay per hour/Second
              Use Case: Long-running applications, custom configurations
          Lambda: 
              Type: Serverless (Event Driven)
              Management: AWS fully manages execution
              Scaling: Auto scales automatically
              Pricing: Pay per execution
              Use cases: short-running tasks, event-driven apps
          Use EC2 for hosting a full-fledged web application that requires persistent storage. Use Lambda for processing image uploads, API requests, or scheduled cron jobs.
### 18. How do you handle high availability and fault tolerance:
          To ensure high availability and fault tolerance, in EC2, best practices include:
            -> Use multiple availability zones (AZs): Deploy instances in atleast AZs for redundancy. Use ELB to distribute traffic across instances.
            -> Auto Scaling Group (ASG): Automatically launch new instances when demand increases. Replace failed instance automatically
            -> Elastic load balancer (ELB): Distributes incoming traffic to healthy instances. Supports health checks to detect failed instances.
            -> Use Amazon RDS Multi AZ for Databases: is using a database, enable multi-AZ for automatic failover.
            -> Backup and Disaster recovery: Regularly take EBS snapshots. Use S3 or Glacier for backup storage.

### 19. What is EC2 Spot Fleet, and how is it different from spot instances:
            A Spot Instance is an individual EC2 instance that AWS provides at a lower cost, but it can be terminated when AWS needs capacity.
            A Spot Fleet is a collection of Spot Instances managed as a single group, providing:
            -> Automatic Instance Diversification – Uses multiple instance types and AZs to improve availability.
            -> Capacity Optimization – Ensures that you get the best price/performance for your workloads.
            -> Fallback to On-Demand Instances – If Spot capacity is unavailable, it can launch On-Demand instances.
                 * Use a Spot Instance if you need a temporary compute resource for running simulations.
                 * Use a Spot Fleet to run large-scale machine learning models, ensuring cost savings and availability by dynamically managing Spot capacity.
### 20. What is difference between EC2 Auto Scaling and Elastic Load Balancing (ELB):
            Auto Scaling ensures the right number of instances are running based on demand. 
            ELB distributes traffic across multiple instances to improve fault tolerance.
## DAY3
### 21. What happens when an EC2 instance running a web application is stopped and restarted:
            The public IP changes unless an Elastic IP is attached.
            EBS volumes remain intact, but instance store data is lost.
            The instance retains its private IP and security group settings
### 22. What is EC2’s default tenancy? What is Dedicated Instance vs Dedicated Host:
            Default Tenancy: EC2 instances run on shared hardware.
            Dedicated Instance: Runs on dedicated hardware for a single AWS account.
            Dedicated Host: Provides a physical server that can be used for compliance and licensing needs.
### 23. How do you encrypt data in EC2:
            EBS Encryption: Encrypts data at rest using AWS KMS.
            SSL/TLS: Encrypts data in transit.
            Instance-level Encryption: Use LUKS (Linux Unified Key Setup) for encrypting volumes.
            S3 Encryption: Use SSE-S3 or SSE-KMS for encrypted object storage.
### 24. What are EC2 Capacity Reservations:
            Capacity Reservations reserve compute capacity in a specific AZ without long-term commitment (unlike Reserved Instances).
            Use Capacity Reservations if you need guaranteed availability for critical applications during peak demand.
### 25. Can you change the instance type of a running EC2 instance:
            No, you must stop the instance first, then modify the instance type.
### 26. What is Amazon EC2 Serial Console:
            A feature that provides low-level access to an instance for troubleshooting without network connectivity.
            If an instance is unresponsive, use Serial Console to check system logs and fix boot issues.
### 27. What is the difference between Replacing Root Volume and Rebuilding an Instance:
            Replacing Root Volume: Creates a new root volume but keeps the instance ID
            Rebuilding an Instance: Terminates the instance and creates a new one
            Use Replace Root Volume if you need to restore a corrupted OS without changing instance settings
### 28. What is Amazon S3:
           Amazon S3 (Simple Storage Service) is an object storage service that allows users to store and retrieve unlimited data. Unlike file or block storage, S3                     stores data as objects in a flat namespace inside buckets. It provides:
                Scalability – Stores unlimited data
                Durability – 99.999999999% (11 9’s) durability
                Security – Supports encryption and IAM policies
                Data Availability – 99.99% availability
                Data Integrity: Uses checksums (MD5, CRC) for corruption detection
### 29. What are the key features of Amazon S3:
              Object Storage – Data is stored as objects with metadata
              Unlimited Storage – No limit on the number or size of objects
              Durability & Availability – 11 9’s durability with automatic replication
              Lifecycle Management – Moves objects between storage classes automatically
              Versioning – Keeps multiple versions of an object
              Replication – Supports Cross-Region and Same-Region Replication
### 30. What are Amazon S3 storage classes:
                   Storage Class                     Use Case                                                 Durability	  Availability	 Cost
                S3 Standard	                    General-purpose	                                          11 9’s	            99.99%	           High
                S3 Intelligent-Tiering	      Auto-moves objects between frequent & infrequent tiers	  11 9’s	            99.9%	           Moderate
                S3 Standard-IA	        Infrequent access (e.g., backups)	                      11 9’s	            99.9%	           Lower
                S3 One Zone-IA	        Infrequent access in a single AZ	                      11 9’s	            99.5%	          Cheaper
                S3 Glacier	                   Archival storage (retrieval in minutes)	                      11 9’s	            99.99%	           Very Low
                S3 Glacier Deep Archive	      Long-term archival (retrieval in hours)	                      11 9’s	            99.99%	           Lowest
