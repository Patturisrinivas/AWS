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
## DAY4
### 31. What is the difference between Object Storage and Block Storage:
          Object Storage (S3) - Stores files with metadata, optimized for scalability.
          Block Storage (EBS, EFS) - Stores data in blocks, ideal for databases and low-latency apps.
          Example:
                Use S3 for storing images, videos, backups
                Use EBS for running a database like MySQL
### 32. What is S3 bucket:
          An S3 bucket is a container where objects are stored. Key bucket properties:
                  Globally unique name (e.g my-aws-bucket)
                  Region-specific storage (e.g us-east-1)
                  access control using IAM policies or ACLs
### 33. How does S3 achieve high durability:
        Stores data across multiple Availability Zones (AZs).
        Automatically replicates objects.
        Uses checksums to detect and fix data corruption
### 34. How does S3 ensure data security:
        IAM Policies – Control access to S3 buckets
        Bucket Policies – Allow/deny access to specific users
        Encryption – Supports server-side (SSE-S3, SSE-KMS) and client-side encryption
        MFA Delete – Requires multi-factor authentication to delete objects
### 35. What is the difference between S3 Object ACL and Bucket Policy:
                Feature                ACL                Bucket policy
                Granularity        Object Level          Bucket leve
                Access Control      Users & Accounts      IAM users, roles
                Complexity          Simple                More flexible
            Use ACLs for fine-grained permissions on specific objects
            Use Bucket Policies to apply rules to the entire bucket
### 36. What is Cross-Origin Resource Sharing (CORS) in S3:
        CORS allows browsers to access S3 resources from different domains. Cross-Origin Resource Sharing (CORS) in Amazon S3 is a security mechanism that allows a web application running on one domain to access resources (like images, fonts, or JSON files) stored in an S3 bucket on a different domain. This is necessary because            browsers enforce the Same-Origin Policy (SOP), which restricts cross-origin requests by default.
        A website hosted on https://example.com wants to load an image from an S3 bucket at https://mybucket.s3.amazonaws.com. Without CORS, the browser blocks the request.         By configuring CORS on the bucket, we can allow specific domains to access the resources.
### 37. How does CORS differ from IAM policies or Bucket Policies:
           IAM/Bucket policies control who can access S3
           CORS controls how cross-origin requests are handled by browsers
### 38. What happens if CORS is misconfigured:
           The browser blocks cross-origin requests, leading to CORS errors in the console
### 39. How do you host a static website on S3:
           Enable static website hosting in bucket settings
           Upload index.html and error.html.
           Set a Bucket Policy to allow public access
### 40. Can S3 host dynamic websites (PHP, Python):
           No. S3 only serves static content. For dynamic content, use Lambda, API Gateway, or EC2
### 41. How do you add HTTPS to an S3 website:
           Use CloudFront with an SSL certificate (ACM)
### 42. How do you prevent unauthorized access:
           Use Bucket Policies, IAM roles, and restrict public access
### 43. What is S3 Event Notification:
           Amazon S3 Event Notifications allow you to automatically trigger actions when specific events happen in an S3 bucket, such as file uploads, deletions, or                    modifications. These events can be sent to various AWS services for further processing.
           how it works: An event occurs in the S3 bucket. S3 detects the event and sends a notification. The notification is delivered to a destination like: 1) AWS Lambda            → Trigger a serverless function. 2) Amazon SNS (Simple Notification Service) → Send notifications. 3) Amazon SQS (Simple Queue Service) → Store events in a queue 
           for processing. Example: Suppose you have an image-processing application where users upload images to an S3 bucket. You can configure an S3 event notification              to trigger an AWS Lambda function that resizes and optimizes the image automatically
### 44. Can S3 Event Notifications trigger multiple destinations:
           No, one event can have only one destination
### 45. How can you ensure reliable processing of S3 events:
           Use Amazon SQS to queue events and prevent loss
## DAY5
### 46. How do you handle duplicate event notifications:
           Implement idempotency in Lambda functions to process events only once
### 47. What are S3 Access Points:
           S3 Access Points provide a customized way to manage access to S3 buckets by allowing you to create dedicated endpoints with specific permissions for different               applications, teams, or workloads. 
           Instead of managing bucket-wide policies, you can create multiple access points, each with its own access policy, simplifying access control in large-scale                  environments.
### 48. When to Use S3 Access Points vs. IAM Roles/Policies:
           Use S3 Access Points when: 
                You need different applications or teams to access the same bucket with different rules.
                You want to restrict access to a VPC
                You want to avoid a complex bucket policy
           Use IAM Roles/Policies when:
                You want to control access at the user or service level across AWS
                You need cross-account access
                You want centralized permission management across services
### 49. Can an S3 bucket have multiple Access Points:
           Yes, you can create multiple access points per bucket for different users/apps
### 50. How do you enforce VPC-only access to an S3 bucket:
           Use an S3 Access Point with VPC restrictions
### 51. Can you use an access point for cross-account access:
           Yes, you can grant access to external AWS accounts via access point policies
### 52. What is Amazon S3 Object Lock:
            S3 Object Lock prevents object deletion or modification for a specified period
### 53. How does S3 Select work:
            S3 Select allows querying only specific data from an object instead of retrieving the full object.
            SELECT * FROM S3Object s WHERE s.city = 'New York'
### 54. What is S3 Multipart Upload:
            Multipart Upload allows uploading large objects in parts to improve performance.
### 55. How does S3 Pricing Work:
            S3 pricing is based on: (1) Storage per GB (varies by storage class) (2) Requests (GET, PUT, DELETE) (3) Data transfer (between AWS regions)
### 56. What is Amazon S3 Access Analyzer:
            It identifies misconfigured bucket policies that allow unintended public access
### 57. What is the difference between ACLs and Security Groups in AWS:
            Access Control Lists (ACLs) and Security Groups are both used for controlling access, but they serve different purposes in AWS.
            An **ACL** in AWS is a rule-based access control mechanism that manages permissions at the resource level. There are two main types:
                 **S3 ACLs** → Control access to individual objects or buckets in Amazon S3.
                 **Network ACLs (NACLs)** → Control inbound and outbound traffic at the subnet level in a VPC.
                  For example, in S3, ACLs are used when you need to grant specific permissions (read, write) on a per-object basis. In a VPC, network ACLs act as a firewall at the subnet level, filtering traffic before it reaches EC2 instances.
            A **Security Group** is a virtual firewall that controls inbound and outbound traffic for EC2 instances or AWS services like RDS. Unlike Network ACLs, which apply at the subnet level, security groups apply directly to an instance and are stateful—meaning if you allow inbound traffic, the response traffic is automatically allowed.
                 For example, if you create a security group for a web server, you can configure it to allow incoming HTTP (port 80) and HTTPS (port 443) traffic but block all other traffic.
             Key Differences:
                    ACLs are stateless, meaning inbound and outbound rules are separate, whereas security groups are stateful, meaning responses are automatically allowed.
                    Network ACLs operate at the subnet level, affecting multiple instances, while security groups apply at the instance level.
                    S3 ACLs provide object-level permissions, but security groups do not apply to S3—they are used for networking and compute resources.

          * Use ACLs when you need fine-grained control over individual objects (S3 ACLs) or subnets (Network ACLs). Use security groups when you want to protect EC2 instances and control which traffic can reach them
### 58. What is the difference between S3 Bucket Policies and IAM Policies:
            S3 Bucket Policy:
                      Applies to specific S3 bucket 
                      Controls access at the bucket level
                      Allows cross-account access
                      Restrict or allow public access to a bucket
            IAM Policy:
                      Applies to IAM users, groups and roles
                      Can control access to multiple AWS services
                      Only applies within the same AWS account
                      Grant users access to multiple AWS services, including S3
            Bucket Policy: Allow public read access to objects in a bucket.
            IAM Policy: Allow an IAM user to list all S3 buckets in the account.
### 59. What is S3 Pre-Signed URL and how does it work:
             A Pre-Signed URL allows temporary, secure access to private S3 objects without making them public
### 60. How does Amazon S3 handle eventual consistency:
             **Strong Consistency**: Any newly created or updated objects are immediately available
             **Eventual Consistency**: Previously, there was a delay in propagating deletes and overwrites across AZs, but AWS now offers strong read-after-write consistency for all operations
## DAY6
### 61. What is the difference between S3 Object Expiration and Lifecycle Policies:
            Object Expiration: Automatically deletes objects after a specified period 
                       Use Case: Delete logs after 30 days
            Lifecycle Policies: Moves objects between storage classes or deletes them
                       Use Case: Move objects to Glacier after 90 days and delete after 1 year
### 62. What is S3 Intelligent-Tiering and when should you use it:
             S3 Intelligent-Tiering automatically moves objects between frequent and infrequent access tiers to optimize costs
### 63. How do S3 Requester Pays Buckets work:
             Normally, the bucket owner pays for storage and data transfer. With Requester Pays, the user downloading the object covers the cost.
### 64. What is the maximum object size allowed in S3:
             5TB per object
             For objects larger than 5GB, use Multipart Upload for better performance
### 65. What are the different types of S3 Encryption:
             SSE-S3: Amazon-managed AES-256 encryption
             SSE-KMS: AWS KMS-managed keys for more control
             SSE-C: Customer-managed keys
             Client-Side Encryption: Data is encrypted before uploading to S3
### 66. How does S3 Object Tagging work:
             Assigns key-value pairs to objects for metadata and categorization
             Helps in access control, cost allocation, and lifecycle rules
### 67. How does S3 Transfer Acceleration work:
             S3 Transfer Acceleration speeds up data uploads using AWS Edge Locations and Amazon CloudFront
### 68. What are S3 Multi-Region Access Points:
             They provide global endpoints to access buckets across multiple regions for faster performance and resilience
### 69. What is AWS Lambda, and how does it work:
             AWS Lambda is a serverless computing service that runs code in response to events. You upload code, configure triggers (such as API Gateway, S3, DynamoDB, etc.), and AWS Lambda automatically executes the function when triggered, managing infrastructure, scaling, and billing based on execution time.
### 70. What are the key benefits of using AWS Lambda:
             No server management – Fully managed by AWS.
             Auto-scaling – Scales automatically based on demand.
             Cost-effective – Pay only for execution time (no idle cost).
             Event-driven – Can be triggered by multiple AWS services.
             Supports multiple languages – Python, Node.js, Java, Go, Ruby, .NET, etc
### 71. What are the supported programming languages in AWS Lambda:
              AWS Lambda supports: Node.js, Python, Java, Go, Ruby, .NET (C#), PowerShell
### 72. How does AWS Lambda pricing work:
              AWS Lambda charges are based on:
                          Number of requests – First 1M requests are free; after that, $0.20 per million requests
                          Execution time – Charged per millisecond based on memory and duration
                          Provisioned Concurrency (if used) – Extra charges apply
### 73. What is the maximum execution timeout for an AWS Lambda function:
              The maximum execution timeout for AWS Lambda is 15 minutes (900 seconds)
### 74. What is the maximum memory allocation for a Lambda function:
              Memory allocation ranges from 128MB to 10GB in increments of 1MB
### 75. How does AWS Lambda scale automatically:
              AWS Lambda scales automatically by creating new instances of the function to handle incoming requests. It follows an event-driven model, where each request can trigger a new execution environment.
             Lambda can scale nearly instantly, handling thousands of concurrent executions by launching additional instances as needed.
             However, it has concurrency limits (1,000 per region by default) and burst limits (500-3,000 instances initially, then 500 per minute). If the limit is reached, requests may be throttled.
             Lambda also optimizes execution by reusing warm instances when possible to reduce cold start delays. Scaling behavior varies based on the event source; for example, API Gateway scales per request, while SQS-based invocations scale based on batch size
