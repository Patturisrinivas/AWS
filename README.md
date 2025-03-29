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
           Duplicate event notifications in AWS can occur due to the at-least-once delivery guarantee of services like SNS, SQS, and EventBridge. To handle duplicates effectively, I use idempotency, deduplication mechanisms, and state tracking to ensure events are processed only once.
           In a project where we processed order events from an SQS queue, we noticed occasional duplicate messages. To resolve this, we used an SQS FIFO queue with MessageDeduplicationId, ensuring that duplicate messages within a 5-minute window were automatically discarded. Additionally, we implemented DynamoDB conditional writes to check if an order ID already existed before processing it, ensuring complete idempotency.
          Idempotency:
                    I design Lambda functions to produce the same result even if the event is processed multiple times.
                    For example, in DynamoDB, I use conditional writes (e.g., attribute_not_exists(id)) to ensure an item is inserted only if it doesn't already exist.
          Deduplication with Message Attributes (SQS FIFO Queues):
                    If using Amazon SQS FIFO queues, I take advantage of the MessageDeduplicationId to ensure duplicate messages within a 5-minute window are ignored.
          Event Deduplication Using External Storage:
                    I use DynamoDB or ElastiCache (Redis) to store event IDs and check if an event has already been processed before proceeding.
                    TTL (Time-to-Live) in Redis helps maintain a temporary cache of processed event IDs.
          Using AWS Lambda Destinations & SQS DLQ:
                    If events are processed asynchronously, I configure Lambda Destinations or an SQS Dead-Letter Queue (DLQ) to track duplicate or failed events and analyze patterns.
          De-duplication via Business Logic:
                    Instead of relying solely on AWS mechanisms, I sometimes implement deduplication at the application level by tracking the state of an operation (e.g., checking if a transaction has already been processed before proceeding).
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
             An S3 Pre-Signed URL is a time-limited, secure URL that allows temporary access to an S3 object without requiring direct AWS credentials. It is commonly used to grant users controlled access to private S3 objects for actions like uploading or downloading files
             A Pre-Signed URL is generated using an IAM user’s or role’s credentials and includes a cryptographic signature. The URL contains:
                    Bucket name & object key – Specifies the file location.
                    HTTP method (GET, PUT, etc.) – Defines the allowed action (upload/download).
                    Expiration time – Determines how long the URL remains valid.
                    Signature – Ensures the request is authenticated.
              Once generated, the user can access the object without needing AWS credentials, as long as the URL is valid
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
## DAY7
### 76. What is an execution environment in AWS Lambda:
            An execution environment is an isolated container where AWS Lambda runs functions, containing the runtime, dependencies, and environment variables.
### 77. What are cold starts in AWS Lambda? How can you reduce them:
            A cold start occurs when AWS Lambda initializes a new execution environment, increasing response time.
            To reduce cold starts:
                        Use Provisioned Concurrency
                        Optimize function size
                        Keep the function warm using scheduled invocations
                        Use lightweight runtimes like Node.js or Python
### 78. Cold Starts vs. Warm Starts:
            Cold Start: If no existing instance is available, Lambda initializes a new one, which may cause a slight delay (100ms to a few seconds).
            Warm Start: If an instance is already running and available, it reuses it, reducing latency.
### 79. What triggers can invoke an AWS Lambda function:
            AWS Lambda can be triggered by:
            Storage & Data Triggers – Lambda can respond to events from services like S3 (object creation/deletion) and DynamoDB Streams (data changes)
            Messaging & Streaming – It can be invoked by SNS (notifications), SQS (queue messages), and Kinesis Streams (real-time data processing).
            API & HTTP Requests – Lambda can be triggered via API Gateway, Application Load Balancer (ALB), and AWS App Runner.
            Scheduled & Event-Based Triggers – Using EventBridge (CloudWatch Events), Lambda can run on a schedule or respond to AWS service changes.
            Security & Management Triggers – Services like AWS Config, Systems Manager, and Secrets Manager can invoke Lambda for compliance and automation tasks.
            Direct Invocation – Lambda can be called manually via the AWS CLI, SDKs, or even by another Lambda function.
            
            The choice of trigger depends on the use case—whether it's processing data, handling API requests, automating workflows, or responding to real-time events
### 80. How would you design a highly available and scalable image processing system using AWS Lambda:
            Scenario: You need to build an image-processing service where users upload images, and AWS Lambda processes them for resizing, watermarking, and storage
             Architecture:
                        User Uploads Image → S3 Bucket
                        S3 Triggers AWS Lambda
                        Lambda Resizes & Adds Watermark
                        Processed Image Stored in Another S3 Bucket
                        SNS Notification or API Gateway Response
             Optimization Considerations:
                        Concurrency Control: Use SQS to avoid throttling issues.
                        Cold Start Optimization: Use Provisioned Concurrency.
                        Error Handling: Configure DLQ (Dead Letter Queue) for failures.
                        Logging & Monitoring: Use CloudWatch & AWS X-Ray for debugging.
### 81. How would you handle large payloads in AWS Lambda:
            Scenario: Your Lambda function needs to process large files (e.g., 1GB CSV data) from an S3 bucket, but the function has a 6MB payload limit.
                        1) Break Large Files into Smaller Chunks
                           Use AWS Glue or AWS Batch instead of Lambda for large processing jobs.
                           Use S3 multipart uploads and S3 Select to process only necessary parts.
                        2) Use S3 to Store Large Payloads & Pass Only References
                           Instead of sending large payloads via API Gateway, store files in S3 and send a reference (URL).
                        3) Leverage Step Functions for Parallel Processing
                           Use AWS Step Functions to divide processing into multiple parallel Lambda executions.
### 82. How would you optimize the cold start time of a high-traffic AWS Lambda function:
            Scenario: Your Lambda function experiences slow response times due to frequent cold starts
                        Optimization Strategies:
                                    Use Provisioned Concurrency – Keeps function instances warm.
                                    Choose a Lightweight Runtime – Node.js/Python have faster startup times than Java/.NET.
                                    Keep Dependencies Minimal – Use Lambda Layers for shared libraries.
                                    Reduce Package Size – Avoid unnecessary dependencies.
                                    Enable SnapStart (for Java functions) – Restores pre-warmed execution environments.
### 83. How do you deploy an AWS Lambda function:
            There are multiple ways to deploy an AWS Lambda function, depending on automation needs and deployment strategy. The key methods include:
                        AWS Management Console – You can manually upload the code as a ZIP file or use the inline editor for small scripts.
                        AWS CLI & SDKs – Using commands like aws lambda create-function or update-function-code, we can deploy Lambda programmatically.
                        Infrastructure as Code (IaC) –
                        AWS CloudFormation – Defines Lambda deployment using YAML/JSON templates.
                        Terraform – Automates Lambda deployment using HCL scripts.
                        AWS SAM (Serverless Application Model) – Simplifies deployment by defining functions, API Gateway, and event sources in a single template.
                        Serverless Framework – Helps deploy and manage Lambda with simple configurations.
                        CI/CD Pipelines (Automated Deployment) – Lambda can be deployed via AWS CodePipeline, GitHub Actions, Jenkins, or GitLab CI/CD, often integrating with AWS CodeBuild.
                        Containerized Deployment – Lambda supports container images (up to 10GB), deployable via Amazon ECR (Elastic Container Registry).
                        
            The choice of deployment method depends on the use case. For quick updates, CLI or console works; for automated deployments, IaC and CI/CD pipelines ensure scalability and consistency.
### 84. What are environment variables in AWS Lambda:
            Environment variables store configuration settings (e.g., API keys, database URLs) that Lambda functions can access at runtime. They are encrypted using AWS KMS
### 85. What is AWS Lambda Layers? How do they help:
            AWS Lambda Layers is a feature that allows you to package and share reusable code, dependencies, or libraries separately from your main function code. Instead of bundling everything into a single deployment package, you can create layers and attach them to multiple Lambda functions.
            How They Help:
                        Reusability – Common dependencies (e.g., SDKs, libraries) can be shared across multiple functions.
                        Smaller Deployment Packages – Reduces function size, improving deployment speed.
                        Easier Updates & Maintenance – Update a layer without modifying every function using it.
                        Security & Versioning – Layers support versioning, making it easy to roll back or upgrade.
               For example, in a DevOps environment, we often use layers to package monitoring agents like Datadog, custom business logic, or Python libraries (e.g., NumPy, Pandas) to avoid bloating each function’s package. This makes deployments more efficient and scalable.
### 86. How do you monitor AWS Lambda performance:
            Monitoring AWS Lambda performance is essential to ensure efficiency, optimize execution, and troubleshoot issues. AWS provides several built-in tools for this:
                         1. AWS CloudWatch Metrics
                                    Tracks key performance indicators like:
                                    Invocation Count – Number of times the function is called.
                                    Duration – Execution time of the function.
                                    Errors & Throttles – Tracks failed invocations and rate limits.
                                    Concurrent Executions – Helps manage scaling limits.
                        2. AWS CloudWatch Logs
                                    Captures function logs for debugging and analysis.
                                    Can be used with AWS Insights to identify slow-running functions.
                        3. AWS X-Ray (Tracing & Debugging)
                                    Helps trace end-to-end request flow to analyze bottlenecks.
                                    Provides visual maps of execution paths for troubleshooting.
                        4. Custom Monitoring & Alerts
                                    CloudWatch Alarms – Set alerts for anomalies (e.g., high error rate, long execution times).
                                    Third-Party Tools – Use Datadog, New Relic, or AWS Lambda Powertools for advanced monitoring.
                        5. Optimizing Performance Based on Metrics
                                    Reduce Cold Starts – Use provisioned concurrency to keep functions warm.
                                    Optimize Memory & CPU – Adjust memory allocation to improve execution time.
                                    Monitor & Tune Timeouts – Avoid unnecessary function execution delays.
                        In a DevOps environment, we integrate Lambda monitoring into CI/CD pipelines and use dashboards for real-time insights, ensuring performance optimization and cost efficiency.
### 87. How can you optimize the performance of an AWS Lambda function:
            Right-Sizing Memory & CPU:
                        AWS Lambda allocates CPU power proportionally to memory. Increasing memory can also improve execution time since it provides more CPU power
                        Use AWS Lambda Power Tuning to find the optimal memory-to-performance ratio
            Minimizing Cold Starts:
                        Cold starts happen when a function is invoked after being idle. To reduce them:
                        Use Provisioned Concurrency to keep function instances warm.
                        Choose smaller deployment package sizes by reducing dependencies.
                        Use lighter runtime environments (e.g., prefer Python over Java if cold start time is critical).
            Optimizing Dependencies:
                        Minimize package size by using Lambda layers for shared dependencies.
                        Remove unused dependencies and use compiled binaries if applicable.
            Reducing Execution Time:
                        Optimize code for efficiency (e.g., avoid unnecessary loops, choose efficient data structures).
                        Use async processing where possible (e.g., SNS, SQS, EventBridge).
            Efficient Networking & API Calls:
                        Reduce the number of network calls and use connection pooling when calling databases.
                        Use Amazon RDS Proxy to optimize database connections.
                        Cache frequent responses using AWS Lambda with Amazon ElastiCache or DynamoDB DAX.
            Monitoring & Profiling:
                        Use AWS X-Ray to analyze performance bottlenecks.
                        Leverage CloudWatch Logs and Metrics to track execution time and optimize accordingly.
            To optimize an AWS Lambda function, I focus on reducing execution time and minimizing cold starts. One of the first things I check is memory allocation—since AWS allocates CPU power based on memory, increasing it slightly can often improve performance. I also use tools like AWS Lambda Power Tuning to find the best balance.
            Another key factor is cold starts. If the function is latency-sensitive, I use Provisioned Concurrency to keep instances warm. In one of my previous projects, we had a Lambda function handling real-time API requests. Initially, cold starts were causing delays, so we implemented Provisioned Concurrency and reduced the deployment package size, cutting response time by 50%.
            Other optimizations I apply include using connection pooling for database interactions (like Amazon RDS Proxy), caching frequently accessed data with DynamoDB DAX, and monitoring performance with AWS X-Ray and CloudWatch. These steps collectively enhance Lambda performance and ensure cost efficiency
### 88. What is AWS Lambda@Edge, and how does it differ from regular Lambda:
            AWS Lambda@Edge is a serverless computing service that runs functions closer to users at AWS Edge locations, rather than in a specific AWS region. It integrates with Amazon CloudFront to customize content delivery, reduce latency, and improve performance."
            The key difference from regular AWS Lambda is that Lambda@Edge is globally distributed, whereas regular Lambda runs in a designated AWS region. It’s mainly used for optimizing web applications by modifying HTTP requests and responses in real time. For example, you can use Lambda@Edge to rewrite URLs, implement security headers, or personalize content dynamically based on user location.
            In one of my projects, we used Lambda@Edge to dynamically redirect users to region-specific websites based on their geolocation, reducing page load times and improving user experience. This wouldn’t have been as efficient with a standard Lambda function because it runs in a fixed region.
### 89. Can AWS Lambda functions run inside a VPC? If so, how do you configure it:
            Yes, configure VPC settings to allow Lambda to access RDS, Redis, or private resources.
### 90. How do you handle errors in AWS Lambda:
            In AWS Lambda, error handling is crucial to ensure reliability and proper execution of functions. I typically handle errors using a combination of built-in AWS features and best practices, such as retries, dead-letter queues (DLQs), and structured logging.
            Key error-handling strategies:
                        Built-in Retries:
                                    AWS automatically retries failed executions for asynchronous invocations (e.g., S3, SNS) twice.
                                    For synchronous invocations (e.g., API Gateway), retries must be managed at the caller level.
                        Dead-Letter Queues (DLQs):
                                    For asynchronous invocations, I configure an SQS queue or SNS topic as a DLQ to capture failed events for later analysis.
                        Lambda Destinations:
                                    Instead of DLQs, I use Lambda Destinations to route failed requests to SQS, SNS, or another Lambda function for processing.
                        Structured Logging & Monitoring:
                                    I enable AWS CloudWatch Logs to track errors and use AWS X-Ray for tracing execution issues.
                                    Implementing structured logging with JSON formatting makes it easier to analyze logs.
                        Custom Exception Handling in Code:
                                    I wrap function logic in try-except blocks (Python) or try-catch (Node.js, Java) to handle known failure scenarios gracefully.
                                    I return custom error messages for better debugging and avoid exposing sensitive information.
                        Circuit Breaker Pattern (Advanced Scenarios):
                                    For functions interacting with external services, I implement a circuit breaker pattern to temporarily stop calls if failures exceed a threshold, preventing cascading failures.
                        For instance, in a project where we processed real-time events using AWS Lambda and SQS, we encountered occasional processing failures. To handle this, we configured a DLQ to capture failed messages and used CloudWatch alarms to notify us when errors exceeded a threshold. This helped us identify issues quickly and retry only the failed events, ensuring smooth processing
## DAY8
### 91. How does AWS Lambda integrate with API Gateway:
            API Gateway can trigger a Lambda function when an HTTP request is received. Lambda processes the request and sends back a response
### 92. What is the difference between synchronous and asynchronous invocation in AWS Lambda:
            Synchronous – Caller waits for the function to complete (e.g., API Gateway, ALB)
            Asynchronous – Events are queued, and Lambda processes them later (e.g., S3, SNS)
### 93. What is the AWS Lambda execution role:
            An IAM role that grants Lambda permissions to access other AWS resources (e.g., S3, DynamoDB)
### 94. What are provisioned concurrency and reserved concurrency in AWS Lambda:
            Provisioned Concurrency – Keeps functions warm to reduce cold starts.
            Reserved Concurrency – Limits the maximum concurrent executions.
### 95. How does AWS Lambda handle retries for failed executions:
            AWS Lambda automatically retries failed executions, but the behavior depends on how the function is invoked.
            For synchronous invocations, like API Gateway or ALB, Lambda doesn’t retry failed requests automatically. The caller (e.g., API Gateway) is responsible for handling retries or failures.
            For asynchronous invocations, like S3 event notifications or EventBridge, Lambda automatically retries the execution twice, with delays between attempts. If all retries fail, the event is sent to a Dead Letter Queue (DLQ) or an EventBridge DLQ, if configured, for further processing.
            For stream-based invocations, like DynamoDB Streams or Kinesis, Lambda keeps retrying until the data expires (which is usually 24 hours) or is successfully processed. If retries keep failing, the event can be sent to a failure destination like an SQS queue for debugging.
            So, the retry behavior depends on whether the function is invoked synchronously, asynchronously, or from a stream, and AWS provides mechanisms like DLQs and failure destinations to handle errors gracefully.
### 96. How do you debug an AWS Lambda function:
            Debugging an AWS Lambda function depends on how it's invoked and where the issue is occurring.
            First, I check the Amazon CloudWatch Logs because every Lambda execution automatically logs request IDs, errors, and print/debug statements. I use console.log in Node.js or print statements in Python to capture specific details.
            Next, I review the AWS X-Ray traces to get a visual breakdown of execution time, latency issues, and bottlenecks, especially for functions interacting with other AWS services.
            If the function is failing due to misconfigurations, I verify the IAM permissions to ensure the function has access to the required AWS resources.
            For event-driven functions, like S3 or SNS triggers, I check the AWS Lambda Dead Letter Queue (DLQ) or EventBridge Failure Destinations for failed events. For stream-based functions (DynamoDB, Kinesis), I analyze the iterator age in CloudWatch to detect processing delays.
            In a local environment, I use the AWS SAM CLI or AWS CDK to invoke and debug the function before deploying it. If it's an API Gateway-integrated function, I enable API Gateway Execution Logging to capture request and response details.
            By combining CloudWatch, X-Ray, DLQs, and local testing tools, I systematically identify and resolve Lambda function issues
### 97. What is AWS Lambda SnapStart:
            AWS Lambda SnapStart is a feature designed to reduce cold start times, specifically for Java-based Lambda functions. Normally, when a Lambda function is invoked after being idle, AWS has to initialize the runtime and dependencies, which causes a delay known as a cold start.
            With SnapStart, AWS takes a snapshot of the fully initialized function, including the runtime, dependencies, and memory state, during the first initialization. This snapshot is then cached and used to quickly restore the function when invoked again, significantly reducing cold start latency.
            SnapStart is particularly useful for latency-sensitive Java applications, such as APIs or event-driven workloads, where quick response times are critical. However, it requires the function to be idempotent because the restored state comes from a snapshot rather than a fresh initialization.
            So, in short, SnapStart helps optimize Java-based Lambda functions by pre-initializing and caching execution environments, leading to faster cold starts
### 98. How can you use AWS Step Functions with AWS Lambda:
            AWS Step Functions can be used with AWS Lambda to orchestrate and manage workflows where multiple functions need to execute in a specific sequence or based on certain conditions.
            Step Functions use a state machine, which defines a series of steps where each step can invoke a Lambda function. This is useful for coordinating complex processes like order processing, data transformations, or machine learning pipelines.
            One key benefit is error handling—Step Functions can automatically retry failed Lambda executions, handle exceptions, and even route errors to alternative workflows. They also support parallel execution, allowing multiple Lambda functions to run concurrently for better efficiency.
            For implementation, I define the workflow using Amazon States Language (ASL), specifying states like Task (for invoking Lambda), Choice (for conditional branching), and Parallel. The execution flow is visualized in the AWS Management Console, making debugging and monitoring easier.
            By integrating Step Functions with Lambda, we can create scalable, serverless workflows with built-in error handling, retries, and state management, reducing the need for custom application logic.
### 99. What are the limitations of AWS Lambda:
            AWS Lambda is a powerful serverless compute service, but it does have some limitations:
            First, there are resource limits—the maximum execution time for a function is 15 minutes, and memory allocation ranges from 128 MB to 10 GB. Also, CPU and network bandwidth scale with the allocated memory, meaning performance is tied to memory settings.
            Second, there's a deployment package limit—the total package size, including layers, cannot exceed 250 MB (unzipped), and individual function code is limited to 50 MB (zipped). This can be restrictive for applications with large dependencies.
            Another limitation is concurrent execution limits—by default, AWS imposes an account-wide 1,000 concurrent execution limit, which can be increased but still requires careful planning to avoid throttling.
            Cold starts can be a challenge, especially for Java and .NET functions, though features like Provisioned Concurrency and SnapStart can help mitigate this.
            Lastly, Lambda has limited execution environments—it only supports certain runtimes like Python, Node.js, Java, Go, and .NET. Running custom binaries or applications requiring persistent state can be complex, often needing additional AWS services like S3, DynamoDB, or EFS.
            Despite these limitations, Lambda remains a great choice for event-driven and serverless applications, as long as resource constraints and architectural considerations are planned for.
### 100. How can you implement CI/CD for AWS Lambda functions:
            To implement CI/CD for AWS Lambda functions, I would use a combination of AWS services like CodePipeline, CodeBuild, and CodeDeploy, along with infrastructure-as-code tools like AWS SAM or Terraform.
            The process starts with version control—I store the Lambda function code in a repository like GitHub, GitLab, or AWS CodeCommit. Whenever changes are pushed, this triggers an AWS CodePipeline execution.
            Next, AWS CodeBuild compiles and packages the code, installs dependencies, and runs unit tests. If the tests pass, the packaged Lambda function is stored in Amazon S3 or ECR (if using container-based Lambda).
            For deployment, AWS CodeDeploy uses deployment strategies like Canary or Linear deployments to gradually roll out the new function version. This helps reduce risk and catch potential issues before fully deploying the new version.
            Additionally, I enable Amazon CloudWatch Logs and AWS X-Ray for monitoring and debugging. I also use feature flags or environment variables to manage configurations without redeploying the function.
            For infrastructure management, I use AWS SAM or Terraform to define the Lambda function, its permissions, and event triggers as code, making deployments consistent and repeatable.
            By integrating these tools, I ensure that every change is automatically built, tested, and safely deployed, reducing manual effort and deployment risks.
### 101. How does AWS Lambda compare to Amazon ECS and AWS Fargate:
            AWS Lambda, Amazon ECS, and AWS Fargate are all compute services, but they serve different use cases.
            **AWS Lambda** is a fully serverless compute service designed for event-driven applications. It automatically scales to handle incoming requests, charges only for execution time, and is ideal for short-lived tasks like API backends, data processing, and event-driven automation. However, it has execution limits, such as a 15-minute timeout, and doesn’t support long-running processes.
            **Amazon ECS** (Elastic Container Service) is a container orchestration service that lets you run and manage containers. It requires managing the underlying EC2 instances (unless using Fargate) and is better suited for applications that need fine-grained control over container runtime, networking, and storage. ECS is ideal for long-running applications, microservices, and batch processing.
            **AWS Fargate** is a serverless compute engine for containers that runs ECS and EKS workloads without managing servers. It’s similar to Lambda in that it removes infrastructure management, but unlike Lambda, it supports long-running containerized applications without execution time limits. It’s a good choice for teams that want the flexibility of containers without managing EC2 instances.
            In short, Lambda is best for event-driven, serverless functions, while ECS with EC2 is for containerized workloads with full control. Fargate sits in between—it provides containerized compute without managing servers but still supports long-running workloads.
### 102. AWS Lambda vs. AWS Step Functions – When should you use each:
            AWS Lambda and AWS Step Functions are often used together, but they serve different purposes and are best suited for different types of workflows.
            **AWS Lambda** is a compute service for running individual, stateless functions in response to events. You should use Lambda when you have a single, isolated task that can run independently without needing to maintain any state between invocations. It’s ideal for event-driven applications, like processing a file uploaded to S3, handling API requests via API Gateway, or performing real-time data processing. Lambda is best when you want quick, efficient execution of tasks, with automatic scaling and a pay-per-use pricing model.
            **AWS Step Functions**, on the other hand, is a service designed for orchestrating workflows that involve multiple steps or tasks, often across different AWS services, including Lambda. Step Functions is ideal when you need to manage more complex workflows or business processes that require different actions in sequence, parallel execution, or branching logic. You would use Step Functions when you need to coordinate a series of Lambda functions or other AWS services (like DynamoDB, SNS, or SQS) in a state machine, handle retries, and manage errors or timeouts.
            In summary, use Lambda for individual, stateless tasks that can run independently, while use Step Functions when you need to build complex workflows involving multiple tasks or services, with built-in error handling, retries, and process orchestration.
### 103. AWS Lambda vs. API Gateway – Are they the same:
            No, AWS Lambda and API Gateway are not the same, though they often work together. They serve different purposes in the AWS ecosystem.
            **AWS Lambda** is a serverless compute service that runs your code in response to events. You define a function (in languages like Python, Node.js, Java, etc.), and Lambda executes it based on triggers, such as an object uploaded to S3, a message in an SQS queue, or a direct HTTP request. It is ideal for running small, stateless functions and performs tasks like processing data, automation, or responding to events.
            **Amazon API Gateway**, on the other hand, is a fully managed service for creating and managing APIs that act as the interface between clients (like web or mobile apps) and backend services. API Gateway enables you to define RESTful or WebSocket APIs, handle routing, and manage API traffic, including authentication, rate limiting, and authorization. It can integrate with AWS Lambda to invoke functions in response to API calls.
            In short, Lambda is the compute service that runs your code, while API Gateway is the service that exposes your functions or services to the internet through an API. They are often used together—API Gateway routes HTTP requests to Lambda functions for backend processing. However, they serve different roles in a serverless architecture
### 104. AWS Lambda vs. AWS Batch – What’s the difference:
            AWS Lambda and AWS Batch are both compute services, but they are designed for different types of workloads and use cases.
            **AWS Lambda** is a serverless compute service that runs code in response to events. It’s best suited for stateless, event-driven tasks that are short-lived, with a maximum execution time of 15 minutes. Lambda is highly scalable, automatically managing the compute resources for you, and you only pay for the actual compute time. It’s ideal for use cases like real-time data processing, API backends, file handling, or event-driven automation, where individual tasks are small and run independently.
            **AWS Batch**, on the other hand, is designed for running large-scale batch processing jobs. It’s more suitable for workloads that require processing a large volume of data in parallel, like scientific computations, video rendering, large data transformations, or machine learning model training. With Batch, you can define the job queues, specify compute environments (e.g., EC2 or Fargate), and manage job dependencies and priorities. Unlike Lambda, AWS Batch can handle long-running jobs and supports stateful, resource-intensive tasks.
            The **key difference **is that Lambda is perfect for lightweight, event-driven, short-lived tasks, whereas AWS Batch is intended for heavy, long-running batch jobs that require more complex orchestration and resource management.
            In summary, use Lambda for quick, event-driven functions and use AWS Batch for large-scale, long-running batch processing workloads that involve heavy computation or data processing.
### 105. AWS Lambda vs. Amazon SQS vs. SNS – How are they related:
            AWS Lambda, Amazon SQS (Simple Queue Service), and Amazon SNS (Simple Notification Service) are all integral parts of the serverless ecosystem, and they can work together to build event-driven, decoupled architectures. Here's how they relate:
            **AWS Lambda** is a compute service that runs your code in response to events. It’s used to process data or execute logic triggered by other services like SQS, SNS, or any other AWS event source. Lambda is typically the "worker" in event-driven architectures, performing tasks based on incoming events.
           **Amazon SQS** is a fully managed message queue service that stores messages until they are processed. It decouples the components of a system by allowing one part of the system to send messages (producers) to a queue, and another part (consumers) to process those messages. Lambda can be triggered to process messages from an SQS queue, which allows for asynchronous message processing with built-in retry logic and dead-letter queue (DLQ) support.
            **Amazon SNS** is a fully managed pub/sub (publish/subscribe) messaging service that enables message broadcasting. SNS allows one-to-many message delivery, meaning you can publish a single message and have it delivered to multiple endpoints (like email, SMS, SQS queues, or Lambda functions). Lambda can be subscribed to an SNS topic, and it will automatically execute the function when a new message is published to the topic.
            In summary, SNS is typically used for pub/sub messaging, where one publisher sends messages to multiple subscribers, while SQS is used for queue-based messaging for decoupling and managing message processing. Lambda can then be used as the compute layer to process messages from either SNS or SQS.
            The three services are often combined in event-driven architectures: you can have SNS publish events, SQS queues store messages for Lambda to process, and Lambda handles the business logic asynchronously.
## DAY9
### 106. AWS Lambda vs. AWS Glue – Which one should you use:
            It really depends on the use case because both services serve different purposes, even though they might seem similar at first glance.
          **AWS Lambda** is best when we need event-driven, serverless compute power to run lightweight scripts or automation. For example, if I need to trigger a function whenever a new file lands in an S3 bucket, perform some quick processing, and store the result in DynamoDB, Lambda is a great choice. It’s cost-effective because we only pay for the execution time, and it scales automatically.
          **AWS Glue**, on the other hand, is more suited for data transformation and ETL (Extract, Transform, Load) workflows. It’s a managed service specifically designed for processing large datasets efficiently, especially when dealing with structured or semi-structured data. If I’m working with big data—like transforming terabytes of raw log files into a structured format for analytics—Glue would be my go-to because it has built-in data cataloging, supports Apache Spark, and integrates well with AWS analytics services.
          So, to sum it up: If I need quick event-driven functions for real-time tasks, I’ll go with Lambda. If I’m handling large-scale ETL operations that require heavy lifting, AWS Glue is the better option.
### 107. AWS Lambda vs. EventBridge – How are they different:
            AWS Lambda and EventBridge serve different roles in an event-driven architecture, but they often work together.
            **AWS Lambda** is a serverless compute service that runs code in response to events. It’s great when I need to execute custom business logic based on triggers like an S3 file upload, a change in DynamoDB, or an API Gateway request. Lambda is responsible for processing the event, performing transformations, and integrating with other AWS services. 
            **EventBridge**, on the other hand, is an event bus that helps route events between AWS services, third-party SaaS applications, and custom applications. It acts as a central hub for event-driven workflows. Instead of writing custom polling mechanisms or manually triggering functions, I can set up rules in EventBridge to listen for specific events and automatically send them to various targets—including Lambda, Step Functions, SNS, and more.
            A simple analogy:
                        EventBridge is like a dispatcher that listens for events and routes them to the right destination.
                        Lambda is like a worker that takes an event and processes it according to the required logic.
                        For example, if an application needs to process customer orders:
            EventBridge can capture events like "New Order Placed" and route them to different services.
            Lambda can take that event, process the order details, update inventory, and send a confirmation email.
            So, if I need to run a function when an event occurs, I’d use Lambda. But if I need to build a loosely coupled event-driven system where multiple services respond dynamically, EventBridge is the better choice.

### 108. AWS Lambda vs. AWS App Runner – When should you use each:
            AWS Lambda and AWS App Runner both offer serverless computing, but they are designed for different types of workloads.
            **AWS Lambda** is best when I need to run short-lived, event-driven functions without managing servers. It’s great for things like processing S3 uploads, handling API requests, transforming data streams, or automating workflows. Since Lambda has a max execution time of 15 minutes, it’s ideal for lightweight, quick-running tasks rather than long-running applications.
            **AWS App Runner**, on the other hand, is better suited for deploying full-fledged web applications and containerized services without worrying about infrastructure management. If I have a containerized application—let’s say a Flask or Node.js app—that needs to be continuously running and handling HTTP requests, I’d go with App Runner. It automatically scales based on traffic and supports long-running workloads, which Lambda isn’t designed for.
            A simple way to think about it:
            Lambda is for running functions on demand in response to events.
            App Runner is for running containerized applications and APIs continuously.
            For example, if I need to process images uploaded to an S3 bucket, Lambda is the better choice since it runs only when needed. But if I’m deploying a backend service that needs to stay up 24/7 and scale automatically with traffic, I’d go with App Runner.
            So, if the workload is event-driven and stateless, I’d use Lambda. If it’s a long-running, containerized web service, App Runner is the better fit
### 109. AWS Lambda vs. AWS Lightsail – What’s the difference:
            AWS Lambda and AWS Lightsail are both cloud computing services, but they serve very different purposes.
            **AWS Lambda** is a serverless compute service designed for event-driven workloads. It’s ideal for running small, stateless functions in response to events like API requests, database updates, or file uploads. Lambda automatically scales and only charges for the time the code is executing, making it highly cost-efficient for intermittent workloads.
            **AWS Lightsail**, on the other hand, is more like a simplified VPS (Virtual Private Server) solution. It provides pre-configured virtual machines, databases, and networking for hosting websites, applications, and small business workloads. Lightsail is a good choice when I need a traditional server environment with predictable pricing, but I don’t want the complexity of configuring EC2 instances and networking from scratch.    
            A simple analogy:
            Lambda is like a light switch that turns on only when needed and shuts off when done, making it cost-efficient for short, event-driven tasks.
            Lightsail is like renting an apartment—it’s always running, offering a fixed-price server environment for web hosting, databases, or applications.
            For example, if I need to run an occasional background job that processes data from an S3 bucket, Lambda is the better choice. But if I want to host a WordPress website or a small web application that runs continuously, Lightsail is the way to go.
            So, if I need an event-driven, fully managed compute service, I’d choose Lambda. But if I need a simple, always-on VPS-like server for hosting or long-running applications, Lightsail is the better fit.
### 110. How do you ensure secure API communication between AWS Lambda and third-party APIs:
            When I integrate AWS Lambda with a third-party API, security is always a top priority. One of the first things I do is make sure that sensitive information, like API keys or OAuth tokens, is never hardcoded. Instead, I store them securely in AWS Secrets Manager or Parameter Store, which allows Lambda to retrieve them only when needed.
            Another key aspect is ensuring that all communication happens over HTTPS. This prevents any unauthorized interception of data in transit. If the API requires authentication, I use secure methods like OAuth or signed requests, depending on what the API supports.
            I also make sure that my Lambda function has the minimum necessary permissions using IAM roles—just enough access to do its job, nothing more. This way, even if something goes wrong, the impact is minimized.
            For reliability, I implement retry logic with exponential backoff to handle transient failures and avoid hitting API rate limits. I also log API interactions using CloudWatch and sometimes enable X-Ray for tracing to monitor performance and troubleshoot issues.
            A real-world example would be integrating Lambda with a payment gateway like Stripe or PayPal. I’d store the API credentials securely, use HTTPS for calls, validate responses to prevent injection attacks, and log all transactions for auditing.
            So overall, security is a mix of secure credential storage, encrypted communication, proper authentication, IAM restrictions, and monitoring. By applying these best practices, I ensure that Lambda communicates with third-party APIs in a safe and efficient manner.
### 111. How do you prevent AWS Lambda from being overwhelmed by a sudden spike in traffic:
            AWS Lambda is designed to scale automatically, but a sudden spike in traffic can still cause issues if not handled properly. When I expect unpredictable traffic patterns, I take a few key measures to prevent Lambda from being overwhelmed.
            First, I set up concurrency limits using Reserved Concurrency. This ensures that my function doesn’t scale beyond a certain number of instances, which is important if it interacts with downstream services like databases that have their own capacity limits. For example, if my Lambda is writing to an RDS database, I’d limit concurrency to prevent too many connections from overwhelming the database.
            For high-throughput applications, I use Provisioned Concurrency, which keeps a set number of Lambda instances warm and ready to handle bursts of traffic without cold starts. This is useful for latency-sensitive applications, like an API backend handling thousands of requests per second.
            If my Lambda is consuming events from an SQS queue, I enable SQS message batching and DLQs (Dead Letter Queues) to handle sudden spikes gracefully. This way, if there’s a backlog of events, Lambda processes them at a controlled rate instead of trying to handle everything at once.
            For API Gateway-based workloads, I configure throttling rules to control the request rate and avoid exhausting Lambda’s concurrency. If I need more resilience, I integrate AWS Step Functions to break down complex workflows into smaller, manageable steps instead of overloading Lambda with heavy processing tasks.
            And of course, I monitor everything using CloudWatch Metrics and Alarms to detect sudden spikes early and scale other parts of my system accordingly.
            So in short, I prevent Lambda from being overwhelmed by using concurrency controls, queue-based processing, API throttling, and proactive monitoring—all while ensuring that downstream systems don’t become bottlenecks.
### 112. How would you implement a real-time serverless data pipeline using AWS Lambda:
            To build a real-time serverless data pipeline using AWS Lambda, I would design an event-driven architecture that processes and analyzes incoming data as soon as it arrives. Let me walk you through a typical implementation using AWS services:
            1. Data Ingestion
            The pipeline starts with a real-time data source. Depending on the use case, this could be:
                        Amazon Kinesis Data Streams for high-throughput event streaming (e.g., IoT data, application logs).
                        Amazon S3 for batch-based real-time processing (e.g., log files, image uploads).
                        Amazon API Gateway for real-time API event ingestion.
                        Lambda is configured as an event trigger for these sources to process data as soon as it arrives.
            2. Data Processing with AWS Lambda
            Once an event is received, Lambda acts as the processing engine, transforming or enriching the data. For example:
                        If it's IoT sensor data from Kinesis, Lambda can parse and filter important metrics before sending them downstream.
                        If it's an image uploaded to S3, Lambda can invoke Amazon Rekognition to analyze it in real-time.
                        If it's log data, Lambda can extract key insights and push structured results to a database.
            3. Storing Processed Data
            After processing, the transformed data needs to be stored for further analysis. Common destinations include:
                        Amazon DynamoDB for structured key-value storage with low-latency querying.
                        Amazon OpenSearch Service for real-time search and analytics.
                        Amazon S3 or Redshift for long-term storage and deeper analysis.
            4. Real-time Notifications & Analytics
            If immediate action is required, Lambda can trigger:
                        Amazon SNS or Amazon SQS to notify users or systems.
                        AWS Step Functions for orchestrating further processing.
                        Amazon QuickSight or OpenSearch Dashboards for visualization.
            5. Monitoring and Scaling
            To ensure reliability and performance, I would:
                        Use CloudWatch Logs & Metrics to monitor execution time and errors.
                        Configure Dead Letter Queues (DLQs) to capture failed messages.
                        Use Auto-scaling with Kinesis and SQS to handle varying loads efficiently.
            Example Use Case:
            For a real-time fraud detection system, I could use:
                        API Gateway to receive transaction data.
                        Lambda to analyze transaction patterns.
                        DynamoDB to store transaction history.
                        SNS to alert on suspicious activity instantly.
            This approach ensures a fully serverless, scalable, and real-time data pipeline with minimal operational overhead. By leveraging AWS Lambda along with event-driven services like Kinesis, S3, and DynamoDB, I can process data in milliseconds without managing servers.
### 113. How would you debug AWS Lambda failures in a production environment:
            Debugging AWS Lambda failures in production is always an interesting challenge because it’s often a mix of logs, metrics, and a bit of intuition. First, I’d start with CloudWatch Logs—that’s usually my go-to. I’d check the logs for any specific error messages or stack traces. If it’s a timeout or memory issue, the logs usually give a pretty good clue.
            Now, if the logs don’t tell me the whole story, I’d move on to CloudWatch Metrics. I’d check things like invocation count, duration, and error count. If I see an increase in errors or a spike in duration, that might indicate the function is hitting a timeout or there’s an external dependency slowing it down.
            If it’s an issue with an upstream or downstream service, I’d check AWS X-Ray. This is super helpful when debugging API Gateway or DynamoDB-related issues. If the function is waiting too long for a response, X-Ray will show me where the delay is happening.
            Then, there’s DLQs (Dead Letter Queues). If the Lambda is triggered by SQS or SNS and keeps failing, I’d check if the messages are landing in a DLQ. That usually means there’s some unhandled exception or retry issue.
            If none of these immediately solve the issue, I’d consider adding more logging—maybe structured logging with request IDs so I can correlate failures across services. Also, if the function is interacting with third-party APIs, I’d check rate limits and authentication issues.
            And of course, if it’s happening across multiple functions, I’d step back and check IAM permissions, VPC configurations, or even deployment rollbacks.
            So yeah, debugging Lambda in production is all about logs, metrics, tracing, and sometimes a little detective work. I always like to take a systematic approach—start with logs, move to metrics, then tracing, and finally check infrastructure issues
### 114. How would you implement blue-green deployment for AWS Lambda:
            So, blue-green deployment for AWS Lambda is all about minimizing downtime and risk when deploying new versions. Since Lambda is versioned natively, I’d take advantage of aliasing to handle the traffic shifting seamlessly. Here’s how I’d do it in production:
            First, I’d deploy the new Lambda version alongside the existing one. In Lambda, each deployment creates a new version, so I don’t overwrite the current production code. Instead, I’d use a Lambda alias—let’s say ‘Prod’—which initially points to the existing stable version (let’s call it v1).
            Once the new version (v2) is deployed, I’d update the alias to shift only a small percentage of traffic—maybe 10%—to v2 while keeping 90% on v1. This can be done using AWS Lambda’s weighted alias feature. Then, I’d monitor CloudWatch logs and metrics, checking for errors, latency, and any unexpected spikes in throttles. If everything looks good, I’d gradually increase the traffic to v2 until it reaches 100%.
            If something goes wrong at any stage, the rollback is instant—I just point the alias back to v1. That’s the beauty of blue-green with Lambda; there’s no waiting for instances to drain connections like with EC2.
            For extra safety, I’d also integrate this with AWS CodeDeploy’s Canary or Linear deployment strategies, so the traffic shift is automated and gradual. This ensures that if any issues arise, CodeDeploy can automatically roll back without manual intervention.
            So, in short—Lambda’s aliasing and versioning make blue-green deployments smooth and risk-free, and with a mix of weighted traffic shifting, monitoring, and rollback mechanisms, we can deploy confidently with minimal impact on users.
### 115. How would you integrate AWS Lambda with an RDS database efficiently:
            So, integrating AWS Lambda with an RDS database efficiently comes down to three key things: connection management, security, and optimizing queries. If I just let Lambda open direct database connections, I could run into connection exhaustion really fast, especially if I have a high number of concurrent executions. RDS has a finite number of connections, and Lambda can scale almost infinitely—so that’s something I have to handle carefully.
            To solve that, I’d use Amazon RDS Proxy. This acts as a connection pooler between Lambda and RDS, which means it efficiently manages and reuses database connections rather than opening a new one every time a Lambda function runs. It also helps with failovers and authentication, which is a bonus.
            For security, I’d avoid storing database credentials inside Lambda. Instead, I’d use IAM authentication with RDS and let Lambda assume a role that grants temporary credentials. This removes the need for hardcoded secrets and makes authentication more secure. If I do need static credentials, I’d store them in AWS Secrets Manager and retrieve them at runtime.
            Now, when it comes to network setup, if my RDS instance is inside a VPC (which it usually is for security), my Lambda function also needs to be inside that VPC with proper security group rules. But to avoid cold start latency issues that come with VPC-enabled Lambdas, I’d ensure that my Lambda uses AWS PrivateLink or a VPC endpoint so it doesn’t need to traverse the internet.
            For performance, I’d keep my queries optimized—things like indexing, limiting the data retrieved, and using read replicas if I have a high-read workload. If my application is read-heavy, I might even introduce Amazon ElastiCache (Redis or Memcached) as a caching layer to reduce the load on RDS.
            So, in summary—use RDS Proxy for efficient connection pooling, IAM for secure authentication, proper VPC setup to avoid cold start delays, and caching where needed. This way, I get the best balance of security, scalability, and performance without running into connection limits or performance bottlenecks
## DAY10
### 116. How do you handle a scenario where AWS Lambda needs to process events exactly once:
            Ensuring exactly-once processing in AWS Lambda can be tricky because Lambda itself is designed to be at-least-once execution. However, we can achieve exactly-once processing by carefully managing idempotency and using services that guarantee deduplication.
            One approach is to use DynamoDB or an external database to track processed events. When a Lambda function is triggered, it first checks if the event has already been processed by looking up a unique identifier—like a message ID or timestamp—in the database. If it finds a match, it simply ignores the event. If not, it proceeds with processing and then records the event as 'processed' in the database.
            Another way is by leveraging SQS with deduplication enabled, specifically FIFO queues. If a message is sent to an SQS FIFO queue, AWS ensures that it's delivered in order and processed only once within the deduplication window.
            For event-driven architectures, AWS EventBridge and Step Functions can also help ensure exactly-once processing by orchestrating workflows and managing state.
            Ultimately, the choice depends on the use case. If I'm working with DynamoDB, I’d use conditional writes. If it's an SQS FIFO queue, deduplication comes built-in. And if I need a more robust workflow, Step Functions can handle state management effectively.
### 117.  How do you ensure AWS Lambda security best practices:
            Security is a top priority when working with AWS Lambda, and I usually take a layered approach to ensure best practices.
            First, I always follow the principle of least privilege when assigning IAM roles to Lambda functions. Instead of giving broad permissions, I ensure each function gets only the exact permissions it needs—nothing more. For example, if a function only needs to read from an S3 bucket, I make sure it doesn’t have write or delete access.
            Another thing I focus on is securing environment variables. Since Lambda often relies on secrets like API keys or database credentials, I never store them in plaintext. Instead, I use AWS Secrets Manager or SSM Parameter Store with encryption enabled. That way, even if someone gains access to the environment variables, the sensitive data remains protected.
            Networking is another aspect—by default, Lambda functions run in a secure AWS-managed environment, but when a function needs to interact with private resources, I place it inside a VPC. I also ensure that security groups and NACLs are tightly controlled to minimize exposure.
            Then there’s logging and monitoring. I always enable AWS CloudWatch Logs for tracking execution details and use AWS Config and AWS Security Hub to continuously monitor for security misconfigurations. And if the function interacts with external APIs or processes user input, I implement validation and sanitization to prevent injection attacks.
            One thing I’ve found really helpful is AWS Lambda’s function URL feature, where authentication is critical. I make sure it's properly secured using IAM or API Gateway authentication to prevent unauthorized access.
            Security is an ongoing process, so I always keep an eye on AWS security advisories and apply patches when necessary.
### 118. How can you automate AWS Lambda deployments:
            Automating AWS Lambda deployments is something I always focus on to ensure consistency, reduce manual effort, and minimize errors.
            For most projects, I use AWS SAM or Terraform. AWS SAM is great because it simplifies defining Lambda functions, API Gateway, and other resources as infrastructure-as-code. With a simple sam build and sam deploy, I can package and deploy everything in a structured way. Terraform is another solid choice when managing larger environments with multiple AWS services since it allows version-controlled, repeatable deployments.
            For CI/CD, I integrate Lambda deployments with AWS CodePipeline and CodeBuild or even tools like GitHub Actions and Jenkins. For example, when I push a new version of my code to a repository, the pipeline automatically packages the Lambda function, runs tests, and deploys it. This helps maintain a smooth, automated release process.            
            When working with multiple environments like dev, staging, and production, I use separate AWS accounts or parameterized deployments so that each environment gets its own configuration without manual changes. Feature toggles also help in rolling out changes gradually.
            Another important aspect is versioning and aliases. Instead of directly updating a live function, I deploy a new version and use aliases like ‘latest’ or ‘prod’ to switch traffic in a controlled way. This makes rollback easier if something goes wrong.
            For zero-downtime deployments, I sometimes use Lambda’s built-in traffic shifting with AWS CodeDeploy. This allows canary or linear deployments where a small percentage of traffic goes to the new version before fully rolling it out. It helps catch issues before they impact all users.
            Automating deployments makes life easier, but I also ensure proper monitoring with CloudWatch and AWS X-Ray to catch issues early. 
### 119. How do you optimize AWS Lambda cost for a high-volume workload:
            Optimizing AWS Lambda costs for high-volume workloads is something I always focus on, especially since Lambda charges are based on execution time, memory allocation, and the number of invocations.
            One of the first things I do is right-size the memory allocation. Many people assume that using lower memory always saves costs, but that’s not always true. Sometimes, increasing memory improves execution speed significantly, reducing the overall billed duration. So, I usually run tests to find the sweet spot between memory and execution time for cost efficiency.
            Another key strategy is reducing the number of invocations. If I’m dealing with a high-frequency event-driven workload, I check whether I can batch process instead of invoking Lambda for every single event. For example, if the function processes messages from SQS or DynamoDB Streams, I increase the batch size to reduce the number of executions.
            For functions that run frequently but don’t require immediate execution, I consider moving them to AWS Fargate or EC2 Spot Instances if they are long-running processes. Lambda is great for short bursts of compute, but for continuous high-volume workloads, sometimes a containerized solution is more cost-effective.
            Then there’s code optimization. I always make sure my Lambda functions are efficient—reducing external API calls, optimizing dependencies, and avoiding unnecessary computations. For instance, if I’m using Python or Node.js, I keep package sizes small so cold starts are faster, and I reuse database connections properly instead of re-establishing them on every invocation.
            Provisioned Concurrency can also help in scenarios with unpredictable traffic, where I need to avoid cold starts but keep costs predictable. I carefully evaluate whether the additional cost of keeping functions warm is justified by performance gains.
            Another trick I use is analyzing cost patterns with AWS Cost Explorer and CloudWatch insights. If I see any unexpected cost spikes, I investigate whether it's due to inefficient code, excessive invocations, or unnecessary retries.
### 120. Can AWS Lambda be used for real-time edge computing? If so, how:
            Yes, AWS Lambda can definitely be used for real-time edge computing, especially with AWS Lambda@Edge and AWS IoT Greengrass.
            Lambda@Edge is great when you need to process requests at AWS CloudFront edge locations, reducing latency by running code closer to users. A good use case is dynamic content personalization—like modifying HTTP headers, rewriting URLs, or even performing security checks before a request reaches the origin server. Since it runs at CloudFront’s edge locations, responses are much faster compared to always reaching back to a centralized server.
            For more advanced real-time edge computing, AWS IoT Greengrass is a better option. It allows running Lambda functions directly on edge devices, even when they’re offline. This is useful in IoT scenarios, like processing sensor data locally before sending only necessary information to the cloud. It helps reduce bandwidth costs and allows real-time decision-making without waiting for a round trip to the cloud.
            So, whether it’s handling user requests at the network edge with Lambda@Edge or running compute workloads on IoT devices with Greengrass, AWS Lambda is definitely a strong candidate for real-time edge computing.
                                                           **or**
            Yes, AWS Lambda can be used for real-time edge computing, mainly through AWS Lambda@Edge. This service allows running Lambda functions at AWS CloudFront edge locations, which helps reduce latency by processing requests closer to the user instead of relying on a central data center.
            A common use case is modifying or personalizing HTTP requests and responses in real time. For example, if a user requests a webpage, Lambda@Edge can dynamically update content, apply security headers, or perform authentication checks before the request reaches the origin server. Another example is caching optimization—Lambda@Edge can decide whether a request should be served from cache or forwarded to the backend, reducing response time.
            Since it runs in CloudFront’s global network of edge locations, it helps offload compute work from origin servers and ensures a faster, more scalable experience for users worldwide
### 121. How would you handle Lambda function timeout issues:
            Handling Lambda function timeout issues depends on what’s causing the delay in execution. Since AWS Lambda has a maximum timeout of 15 minutes, the goal is to optimize performance so that functions complete within the expected time.
            One of the first things I do is check if the function is waiting on an external service, like a database query or an API call. If an API is slow to respond, I either optimize the request—like reducing payload size—or use retries with exponential backoff instead of waiting indefinitely. In some cases, moving to asynchronous processing using SQS or EventBridge helps, so the function doesn't have to wait for a response before continuing.
            Another common issue is inefficient code. I make sure that the function is not performing unnecessary computations or loading large dependencies. For example, if I’m using Python or Node.js, I minimize package size and ensure database connections are reused instead of reconnecting on every invocation.
            Memory allocation also plays a big role. Since Lambda execution time is directly affected by memory, I often run tests to find the right balance—sometimes increasing memory actually reduces runtime, which lowers both cost and the risk of timeouts.
            If timeouts still occur and the function needs more time, I consider breaking the task into smaller executions using Step Functions, which allow long-running workflows by chaining multiple Lambda functions together.
            Monitoring is key, so I always check CloudWatch logs and AWS X-Ray traces to see where the function is slowing down. This helps pinpoint exactly which part of the execution is causing delays.
            Ultimately, the approach depends on the workload. If it’s an API-driven function, I optimize external calls. If it’s a long-running job, I break it into smaller tasks. And if it’s a resource issue, I fine-tune memory and code efficiency to keep execution times under control.
### 122. How does AWS Lambda integrate with DynamoDB Streams:
            AWS Lambda integrates seamlessly with DynamoDB Streams to enable real-time event-driven processing. Whenever data in a DynamoDB table changes—like an item being inserted, updated, or deleted—DynamoDB Streams captures those changes as a sequence of events. Lambda can be triggered automatically to process those events without needing to poll the database.
            For example, let’s say there’s an e-commerce application where orders are stored in a DynamoDB table. Whenever a new order is placed, the change event is captured by DynamoDB Streams, which then triggers a Lambda function. That function could be used to send a confirmation email, update an analytics dashboard, or even trigger downstream workflows like inventory management.
            The great thing about this integration is that Lambda processes records in batches, and I can configure things like batch size and parallelism to control performance. By default, it uses an at-least-once delivery model, so I always ensure my function is idempotent—meaning it can handle duplicate events gracefully.
            I also monitor this setup using CloudWatch Logs to track function execution and DynamoDB metrics to check stream processing latency. If high traffic is expected, enabling on-demand scaling for DynamoDB and tuning Lambda’s concurrency settings helps handle the load efficiently.
            So, overall, this integration is a powerful way to react to database changes in real-time without building a separate polling mechanism or additional infrastructure.
### 123. How does AWS Lambda handle concurrency and scaling:
            AWS Lambda handles concurrency and scaling automatically, which makes it great for highly scalable applications without needing to manage servers.
            By default, every time a Lambda function is triggered, AWS spins up an execution environment to handle the request. If multiple requests come in at the same time, Lambda launches multiple instances in parallel, up to the account’s concurrency limit. So if a function gets 100 requests at once, AWS will scale up by running 100 concurrent instances of that function.
            Now, Lambda does have a concept called reserved concurrency and provisioned concurrency. Reserved concurrency ensures that a specific function always has a certain number of instances available, preventing it from being throttled by other workloads. Provisioned concurrency, on the other hand, keeps function instances warm, reducing cold start times—this is useful for latency-sensitive applications like APIs.
            Scaling is also event-driven. For example, if a function is triggered by an API Gateway, each HTTP request can invoke a new instance of the function. If it’s processing SQS messages, the number of concurrent executions scales based on the queue size. However, to prevent overwhelming downstream systems like databases, I sometimes limit concurrency using concurrency settings or introduce SQS and EventBridge to throttle and buffer requests.
            One key thing to watch out for is the regional concurrency limit, which applies across all Lambda functions in an AWS account. If too many functions are invoked at once, they can hit this limit and get throttled, so I always monitor metrics in CloudWatch and adjust limits as needed.
            So, in short, Lambda scales automatically, but fine-tuning concurrency settings helps optimize performance and prevent throttling in high-traffic scenarios.
### 124. How does AWS Lambda integrate with REST APIs:
            AWS Lambda integrates with REST APIs primarily through Amazon API Gateway, which acts as a front door for HTTP requests and triggers the Lambda function whenever an API request comes in.
            For example, let’s say I’m building a serverless application where users can fetch and update their profile information. I’d set up an API Gateway with different REST endpoints, like GET /user/{id} to fetch user data and POST /user to update it. Each of these endpoints would be connected to a specific Lambda function, which then processes the request and interacts with a database like DynamoDB.
            API Gateway handles request routing, authentication, and even request/response transformations before passing the event to Lambda. The function then runs the business logic and returns a response that API Gateway formats and sends back to the client.
            One thing I always consider is performance optimization. If low latency is critical, I enable Lambda function URLs for direct HTTPS access or use Provisioned Concurrency to reduce cold start times. If API Gateway needs to handle high traffic, I enable caching or configure throttling to prevent excessive requests from overwhelming the backend.
            For authentication and security, API Gateway supports IAM policies, JWT authentication with Amazon Cognito, or custom authorizers using Lambda. If I need fine-grained access control, I might implement a Lambda authorizer to validate tokens before processing API requests.
            This integration makes it really easy to build scalable, serverless REST APIs without managing infrastructure, and it works well with other AWS services like Step Functions, S3, or EventBridge for more complex workflows.
### 125. How do you implement versioning and rollback strategies for AWS Lambda:
            AWS Lambda provides built-in versioning, which helps in maintaining immutable versions of a function. Every time we publish a version, it gets a unique number, and the $LATEST version always points to the most recent one. However, for production environments, we typically use aliases to point to specific stable versions instead of $LATEST to avoid unintended changes.
            When it comes to rollback strategies, the easiest way is to update the alias to point back to the previous stable version. If a new deployment causes issues, we don’t have to redeploy—just shifting the alias back instantly restores the older version. Another approach is using traffic shifting with weighted aliases. This allows us to gradually roll out a new version by sending, say, 10% of traffic to the latest version and keeping 90% on the stable one. If everything looks good, we gradually increase the traffic, but if we notice errors, we can immediately revert without downtime.
            This combination of versioning, aliases, and traffic shifting ensures smooth deployments and quick recovery if needed, making Lambda functions more reliable in production environments.
### 126. What are the latency differences between Lambda@Edge and normal AWS Lambda:
            The key difference in latency between AWS Lambda and Lambda@Edge comes down to where the function runs. Regular AWS Lambda functions run in specific AWS Regions, which means if a user is far from that region, there's a bit of added latency due to network travel time.
            On the other hand, Lambda@Edge runs at AWS edge locations, which are much closer to end users. This significantly reduces latency, especially for applications that need to process requests at the edge—like modifying HTTP responses, authenticating users, or handling real-time personalization. Since the function executes at a nearby edge location instead of a central AWS Region, the response time is much faster.
            Another factor is cold starts. While both Lambda and Lambda@Edge have cold starts, Lambda@Edge tends to have slightly lower cold start times since it's optimized for quick execution at the edge. However, it also has some limitations, like execution time and resource constraints compared to standard Lambda.
            So, if low latency is the goal—especially for global users accessing content or APIs—Lambda@Edge is often the better choice
### 127. What happens if AWS Lambda exceeds its memory allocation:
            So, in AWS Lambda, the memory allocation isn't just about RAM—it also determines CPU power, network bandwidth, and disk I/O performance. But if a Lambda function exceeds its allocated memory, it doesn’t get throttled or slowed down—it simply gets terminated with an OutOfMemoryError. Basically, the execution stops, and AWS logs the error in Amazon CloudWatch, so you can troubleshoot and adjust accordingly.
            One way to avoid this is by monitoring memory usage with AWS CloudWatch metrics. There’s a metric called MaxMemoryUsed that helps track how close the function gets to its limit. If I notice a function frequently hitting, say, 90% or more of its allocated memory, I’d probably increase the allocation slightly to avoid unexpected failures. AWS also has an auto-tuning tool called Lambda Power Tuning, which helps find the optimal memory setting for better performance and cost efficiency.
### 128. How does AWS Lambda handle retries and failures for synchronous vs. asynchronous invocations:
            AWS Lambda handles retries and failures differently based on whether the invocation is synchronous or asynchronous.
            For **synchronous invocations**, the service that calls Lambda—like API Gateway or an application using the AWS SDK—has to handle errors and decide whether to retry. Lambda itself doesn’t automatically retry failures in this case. If the function times out, throws an error, or runs into an issue like insufficient memory, the caller receives the error response directly and has to handle the retry logic.
            On the other hand, **asynchronous invocations**, such as those triggered by S3 events or EventBridge, work differently. AWS Lambda automatically retries the execution twice in case of failure, meaning the function gets three attempts in total. If all retries fail, the event is either dropped or sent to a Dead Letter Queue (DLQ) or an EventBridge DLQ if configured. A better approach is to use Lambda Destinations, which allow capturing both successful and failed invocations and routing them to services like SQS, SNS, or another Lambda function for further handling.
            So, in summary, synchronous invocations rely on the caller for retries, while asynchronous invocations have built-in retry mechanisms and optional failure handling through DLQs or Destinations.
### 129. How would you optimize AWS Lambda cost for batch processing workloads:
            Optimizing AWS Lambda costs for batch processing comes down to a few key factors: memory allocation, execution time, and how the workload is distributed.
            First, memory tuning is critical. Since AWS Lambda pricing is based on memory and execution time, I’d use AWS Lambda Power Tuning to find the optimal balance. Sometimes increasing memory reduces execution time significantly, lowering the overall cost.
            Next, I’d consider using AWS Step Functions if the batch process involves multiple Lambda executions. Step Functions allow better orchestration and reduce redundant invocations, avoiding unnecessary Lambda costs.
            For large-scale batch processing, I’d evaluate whether Lambda is even the best option. AWS Batch or Fargate might be more cost-effective for workloads that require high CPU or extended run times beyond Lambda’s 15-minute limit.
            Lastly, enabling Compute Savings Plans or using Provisioned Concurrency with a reserved capacity model can help reduce costs if the batch processing workload is predictable and runs frequently.
            So, the key is to fine-tune memory, reduce execution time, consider alternative AWS services if needed, and leverage cost-saving plans where applicable.
### 130. How does AWS Lambda handle environment variables securely:
            AWS Lambda provides a secure way to handle environment variables by encrypting them at rest and in transit. By default, environment variables are encrypted using AWS Key Management Service (KMS) before being stored. When the function runs, Lambda decrypts them and makes them available to the execution environment.
            For added security, if the environment variables contain sensitive information like API keys or database credentials, it’s best to use AWS Secrets Manager or AWS Systems Manager Parameter Store instead. These services store and manage secrets securely, and the Lambda function can retrieve them at runtime using fine-grained IAM permissions.
            Additionally, access to environment variables can be restricted using IAM policies to ensure only authorized functions or users can modify them. Combined with proper logging and monitoring in CloudWatch, this ensures that sensitive data remains protected.
            So, while Lambda encrypts environment variables by default, best practices involve using dedicated secret management services and applying least privilege access controls to keep them even more secure.
## DAY11
### 131. What is AWS IAM:
            AWS Identity and Access Management (IAM) is a service that enables secure access control to AWS resources. It allows you to create and manage users, groups, roles, and policies to define permissions for accessing AWS services. IAM is a global service and does not require any additional costs
### 132. What are IAM users, groups, and roles:
            **IAM User**: A user represents an individual who needs access to AWS. Each user has unique credentials (username and password or access keys).
            **IAM Group**: A collection of IAM users that share the same permissions. This helps manage access efficiently.
            **IAM Role**: A role is an identity that can be assumed by trusted entities (users, applications, AWS services). Unlike users, roles do not have long-term credentials; they provide temporary permissions.
### 133. What are IAM policies? How do they work?
            IAM policies are JSON documents that define permissions for users, groups, or roles. A policy consists of statements that include:
                        Effect: Either Allow or Deny access.
                        Action: Specifies the AWS service and API action (e.g., s3:PutObject).
                        Resource: Defines the AWS resource the policy applies to.
                        Condition: (Optional) Adds constraints like IP addresses or MFA authentication
### 134. What is the difference between an inline policy and a managed policy:
            Inline Policy: A policy directly attached to a single IAM user, group, or role. These are tightly coupled with the entity
            Managed Policy: A standalone policy that can be attached to multiple users, groups, or roles. AWS provides AWS-managed policies, while customers can create custom-managed policies
### 135. What is an IAM role and how is it different from an IAM user:
            An IAM user has permanent credentials (passwords or access keys) and is meant for human access.
            An IAM role does not have long-term credentials and is assumed temporarily by AWS services, users, or applications. Roles use temporary security credentials provided by AWS Security Token Service (STS).
### 136. How does IAM support Multi-Factor Authentication (MFA):
            IAM allows enabling MFA for users to add an extra security layer. It requires users to provide a second factor (such as a one-time password from an MFA device) in addition to their password. AWS supports:
                        Virtual MFA devices (e.g., Google Authenticator).
                        Hardware MFA devices.
                        FIDO Security Keys.
### 137. What are IAM permission boundaries:
            A permission boundary is an advanced IAM feature that restricts the maximum permissions a user or role can have, regardless of other attached policies. It prevents privilege escalation by ensuring users/roles cannot exceed defined access limits.
### 138. What is the IAM policy evaluation logic:
          When a user or role requests access, AWS IAM evaluates policies using the following rules:
            **Explicit Deny**: If any policy explicitly denies access, the request is denied.
            **Explicit Allow**: If there is an allow statement and no explicit deny, the request is allowed.
            **Implicit Deny**: If a request is not explicitly allowed, it is denied by default.
### 139. How does IAM integrate with AWS Organizations:
            AWS Organizations allow centralized management of multiple AWS accounts. IAM integrates with Organizations using Service Control Policies (SCPs), which set permission guardrails for accounts within the organization. SCPs do not grant permissions but restrict the maximum permissions accounts can have.
### 140. What is AWS IAM Identity Center (SSO), and how does it work:
            AWS IAM Identity Center (previously AWS SSO) provides centralized access management for AWS accounts and business applications. It allows users to sign in once and access multiple AWS accounts without needing IAM users. It supports integration with Active Directory and third-party identity providers.
## DAY12
### 141. What are AWS IAM session policies:
            IAM session policies are temporary policies applied when assuming a role. They limit permissions during a session, even if the role has broader permissions. This is useful for providing least-privilege access dynamically.
### 142. What is the difference between an IAM policy and an SCP:
            **IAM Policy**: Grants or restricts permissions for IAM users, groups, and roles within an AWS account.
            **Service Control Policy (SCP)**: Applies to AWS accounts within an Organization to set permission limits. SCPs do not grant permissions but define what actions are allowed at the account level
### 143. How do IAM Roles work with EC2 instances:
            IAM roles can be assigned to EC2 instances using Instance Profiles. This allows applications running on EC2 to access AWS services securely without needing access keys. The EC2 instance fetches temporary credentials from the instance metadata service (IMDSv2 recommended)
### 144. How do you enforce least privilege access in AWS IAM:
            To implement least privilege access:
                        Assign only necessary permissions using granular policies.
                        Use IAM roles instead of long-term access keys.
                        Implement IAM permission boundaries.
                        Use MFA for sensitive actions.
                        Regularly audit permissions using AWS IAM Access Analyzer.
### 145. How do you troubleshoot IAM access issues:
            Check IAM Policies – Ensure the user/role has the necessary permissions.
            Look for Explicit Denies – Any deny in a policy overrides allows.
            Validate Resource Policies – Services like S3, KMS, and Lambda can have resource-based policies that might block access.
            Use IAM Policy Simulator – Helps test and debug policies.
            Verify Service Control Policies (SCPs) – If using AWS Organizations, SCPs might restrict permissions.
### 146. Can you give an example of a scenario where you would use an IAM Role instead of an IAM User:
            A common scenario is when an application running on an EC2 instance needs access to an S3 bucket. Instead of storing access keys in the instance, we attach an IAM Role to the EC2 instance. The application can then assume the role and retrieve temporary credentials securely.
### 147. What happens if an IAM user is part of multiple groups with conflicting permissions:
            IAM follows a default deny rule. If one policy allows an action and another policy denies it, the explicit Deny always takes precedence. If no explicit allow or deny is mentioned, the action is denied by default.
### 148. Can an IAM role assume another IAM role? If yes, how:
            Yes, IAM roles can assume other roles using the sts:AssumeRole API. This is commonly used in cross-account access scenarios where one AWS account needs temporary access to another. The role being assumed must have a trust policy allowing the first role to assume it.
### 149. What is the difference between an IAM user policy and a resource-based policy:
            **IAM User Policy**: Attached to IAM users, groups, or roles to define what AWS resources they can access.
            **Resource-Based Policy**: Attached directly to AWS resources (e.g., S3 bucket, Lambda function, KMS key). They specify who can access the resource and what actions they can perform.
### 150. What is AWS IAM Access Analyzer, and how does it work:
            AWS IAM Access Analyzer is a tool that helps identify and analyze access to AWS resources. It:
                        Scans policies to check if resources (e.g., S3 buckets, IAM roles) are accessible outside the account.
                        Identifies unintended public access or overly permissive policies.
                        Provides actionable insights for tightening security
## DAY13
### 151. What is the difference between AWS STS (Security Token Service) and IAM Roles:
                        AWS STS: A service that issues temporary security credentials (valid for up to 12 hours).
                        IAM Role: An identity that can be assumed to get temporary credentials from STS.
            IAM roles use STS under the hood to provide temporary access to AWS services.
### 152. How do cross-account IAM roles work:
            To allow access between AWS accounts:
                        The target account creates an IAM role with a trust policy allowing the source account to assume it.
                        The source account uses sts:AssumeRole to get temporary credentials.
                        The role grants permissions based on the attached policies.
### 153. How do you restrict IAM access to specific IP addresses:
            By using IAM policy conditions with the aws:SourceIp key.
### 154. How do IAM Roles work with Lambda functions:
            When creating an AWS Lambda function, you must assign an execution role. This IAM role grants the function permission to access AWS services like S3, DynamoDB, or CloudWatch logs. The Lambda function assumes this role when executing.
### 155. What are IAM Service-Linked Roles:
            IAM Service-Linked Roles are predefined roles created and managed by AWS services (e.g., AWS Config, AWS Organizations). They allow AWS services to perform actions on your behalf without requiring manual role configuration.
### 156. What happens if an IAM user loses their MFA device:
            The user cannot log in until MFA is disabled or reset.
            An IAM administrator must disable or reconfigure MFA for the user.
            Best practice: Enable multiple MFA devices or use account recovery options.
### 157. Can IAM policies be used to control access to AWS Billing and Cost Management:
            Yes, but AWS billing data is account-wide and requires special permissions. Users must have:
                        aws-portal:ViewBilling to view billing information.
                        aws-portal:ModifyBilling to change payment settings.
### 158. What is the IAM best practice for managing access keys:
            Avoid long-term access keys; prefer IAM roles.
            Rotate access keys periodically.
            Use IAM policies to restrict API access.
            Store keys securely using AWS Secrets Manager or Parameter Store.
### 159. Can you assign IAM permissions to a specific AWS Region:
            Yes, IAM supports regional restrictions using condition keys
                        "Condition": { "StringEquals": { "aws:RequestedRegion": "us-east-1" } }
                        This ensures users can only perform actions in us-east-1.
### 160. What are IAM session duration limits:
            By default, IAM role sessions last one hour.
            The maximum session duration can be extended up to 12 hours using IAM settings.
            Temporary credentials expire automatically after the session duration ends.
## DAY14
### 161. What is a VPC in AWS:
          A Virtual Private Cloud (VPC) in AWS is a logically isolated network within the AWS cloud that enables users to launch AWS resources in a customized network environment. It allows complete control over networking, including IP addressing, subnets, route tables, security groups, and network ACLs. Essentially, a VPC acts as a private data center in the cloud, ensuring secure communication between resources
### 162. What are the main components of an AWS VPC:
          An AWS VPC consists of several essential components:
                    Subnets – Divisions of the VPC into smaller network segments (public/private).
                    Route Tables – Define the rules for traffic routing between subnets and external networks.
                    Internet Gateway (IGW) – Enables communication between VPC resources and the internet.
                    NAT Gateway/Instance – Allows private subnet instances to access the internet while keeping them private.
                    Security Groups – Act as a virtual firewall at the instance level.
                    Network ACLs (NACLs) – Provide an additional layer of security at the subnet level.
                    Elastic IP (EIP) – A static IP address for instances.
                    VPC Peering & Transit Gateway – Enables communication between VPCs.
### 163. What is the difference between a Security Group and a Network ACL:
          **Feature**	            **Security Group**	                                   **Network ACL**
             Level	                        Instance-level	                                               Subnet-level
          Stateful/Stateless	       Stateful (Automatically allows return traffic)	Stateless (Explicitly allow/deny both inbound and outbound rules)
            Rules	                       Only allow rules	                                         Both allow and deny rules
          Default behavior	      Denies all inbound traffic, allows all outbound traffic	Allows all inbound and outbound traffic by default
          Evaluation order	           Evaluates all rules before deciding	                   Rules evaluated in numerical order
     Security groups are used for fine-grained instance protection, whereas NACLs provide broader control at the subnet level.
### 164. What is the difference between a Public and a Private Subnet:
          Public Subnet: Contains resources that need direct access to the internet. It has a route to an Internet Gateway (IGW), allowing inbound and outbound communication over the internet.
          Private Subnet: Hosts resources that should not have direct internet access, such as databases. It does not have a direct route to an IGW. Instead, if outbound internet access is needed, a NAT Gateway is used.
### 165. What is a NAT Gateway, and how does it work:
          A NAT (Network Address Translation) Gateway allows instances in a private subnet to access the internet while keeping them hidden from inbound internet connections. It enables outbound traffic but blocks unsolicited inbound traffic.
          It works by:
                    Receiving a request from a private instance.
                    Replacing the private IP with its Elastic IP.
                    Sending the request to the internet.
                    Receiving the response and forwarding it back to the private instance.
                    This is crucial when private instances need software updates or access to external APIs.
### 166. How does VPC Peering work, and when would you use it:
          VPC Peering is a networking connection between two VPCs that allows them to communicate privately using private IP addresses as if they were in the same network.
          It is useful when:
                    You have multiple AWS accounts and want them to share resources.
                    You need secure communication between different departments' VPCs.
                    You want to avoid public internet exposure while transferring data.
                    However, VPC Peering does not support transitive routing, meaning if VPC A is peered with VPC B and B is peered with VPC C, A cannot communicate with C unless explicit peering is established.
### 167. What is a Transit Gateway, and how is it different from VPC Peering:
          AWS Transit Gateway is a scalable network hub that allows multiple VPCs and on-premises networks to communicate through a single gateway. Unlike VPC Peering, it supports transitive routing, simplifying complex network architectures.
              Differences:
                    VPC Peering is a direct connection between two VPCs (one-to-one).
                    Transit Gateway allows many-to-many communication, acting as a central hub.
                    It is recommended for large-scale architectures with multiple VPCs needing seamless communication.
### 168. What are VPC Endpoints, and why are they used:
          VPC Endpoints enable private connectivity between a VPC and AWS services without requiring the internet, VPNs, or NAT Gateways. There are two types:
                    Interface Endpoints – Use private IPs and Elastic Network Interfaces (ENIs). Example: Connecting to AWS S3, DynamoDB, etc.
                    Gateway Endpoints – Work at the route table level and only support S3 and DynamoDB.
          Benefits:
                    Eliminates the need for an Internet Gateway or NAT Gateway.
                    Reduces data transfer costs by avoiding public internet traffic.
                    Enhances security by keeping traffic within AWS.
### 169. What is the difference between an Internet Gateway and an Egress-Only Internet Gateway:
          **Internet Gateway** (IGW): Enables both inbound and outbound internet access for IPv4 traffic.
          **Egress-Only Internet Gateway** (EIGW): Designed for IPv6 traffic, allowing only outbound communication.
           Egress-Only IGW is used when instances in a private subnet need outbound internet access over IPv6 without exposing them to incoming connections.
### 170. How do you secure a VPC:
          To secure a VPC, I follow these best practices:
                    Use Security Groups and NACLs to restrict access at different layers.
                    Minimize public exposure by keeping critical resources in private subnets.
                    Use VPC Endpoints to access AWS services privately.
                    Enable VPC Flow Logs for network monitoring and auditing.
                    Use IAM roles and policies to enforce least privilege access.
                    Restrict outbound traffic using NAT Gateways and Firewall rules.
                    Use AWS WAF and Shield for DDoS protection.
                    By implementing these, we ensure secure and controlled network traffic within the VPC.
## DAY15
### 171. What is Elastic Load Balancing (ELB) in AWS:
          AWS Elastic Load Balancing (ELB) is a managed service that automatically distributes incoming traffic across multiple targets, such as EC2 instances, containers, and IP addresses. It enhances application availability, fault tolerance, and scalability by balancing the load among multiple resources in one or more availability zones.
          ELB provides four types of load balancers:
                    Application Load Balancer (ALB) – Best suited for HTTP/HTTPS traffic with advanced routing features.
                    Network Load Balancer (NLB) – Handles TCP, UDP, and TLS traffic with ultra-low latency.
                    Gateway Load Balancer (GWLB) – Used for deploying and scaling third-party virtual appliances.
                    Classic Load Balancer (CLB) – Legacy option that supports both HTTP/HTTPS and TCP traffic.
### 172. What are the benefits of using AWS ELB:
          AWS ELB provides several benefits, including:
                    Automatic scaling – It dynamically scales to handle varying traffic loads.
                    High availability – Ensures failover across multiple Availability Zones (AZs).
                    Security integration – Works with AWS WAF, Shield, and ACM for enhanced security.
                    Health checks – Automatically detects and removes unhealthy targets.
                    SSL termination – Offloads SSL decryption to reduce application server load.
                    Ease of management – Fully managed by AWS, eliminating the need for manual configuration.
### 173. What are the differences between ALB, NLB, and CLB:
          **Feature**	             **ALB (Application LB)**	                   ** NLB (Network LB)**	          ** CLB (Classic LB)**
          **Protocol**	                      HTTP, HTTPS	                       CP, UDP, TLS	                    HTTP, HTTPS, TCP
          **Routing**	                Layer 7 (Application)	                    Layer 4 (Transport)	                    Layer 4 & 7
          **Performance**	                    Good for web apps	                    High-performance,                     low latency	General-purpose
          **Use Case**	                 Web applications, microservices	       Real-time streaming, gaming, IoT	         Legacy applications
          **SSL Termination**	                         Yes	                                        No	                              Yes
          AWS recommends ALB for modern applications, while NLB is best for ultra-low latency and high-throughput scenarios.
### 174. What is a Target Group in AWS Load Balancing:
          A Target Group is a logical grouping of backend resources, such as EC2 instances, Lambda functions, or IP addresses, that receive traffic from a load balancer.
          Each target group is associated with health checks to monitor resource availability. A load balancer routes traffic to only healthy targets within the group.
          Example:
          An ALB can route traffic to multiple target groups based on URL paths (/api → API servers, /images → Image servers).
          An NLB can distribute TCP traffic among a group of EC2 instances.
### 175. How does AWS ELB perform health checks:
          ELB uses health checks to monitor the status of targets (EC2, Lambda, etc.). It periodically sends requests to each registered target to ensure they are healthy.
          Health checks have the following parameters:
                    Protocol & Port – Defines the type of request (HTTP, TCP) and port number.
                    Healthy/Unhealthy Threshold – Number of consecutive successful/failed checks before marking a target as healthy/unhealthy.
                    Interval – Frequency of health check requests.
                    Timeout – How long to wait for a response before considering the check failed.
                    If a target fails multiple health checks, it is removed from service, and traffic is rerouted to healthy instances.
### 176. How does SSL termination work in AWS ELB:
          SSL termination is the process of decrypting SSL/TLS traffic at the load balancer instead of the backend servers. This reduces the computational load on application servers.
          ALB & CLB support SSL termination via AWS Certificate Manager (ACM) or manually uploaded certificates.
          NLB does not support SSL termination; it passes encrypted traffic to backend instances.
          Benefits:
                    Improves application performance.
                    Allows centralized certificate management.
                    Enables HTTP to HTTPS redirection at the load balancer level.
### 177. How does ALB handle host-based and path-based routing:
          Host-Based Routing: Routes requests based on the domain name in the request header.
                    Example: api.example.com → API servers, blog.example.com → Blog servers.
          Path-Based Routing: Routes requests based on the URL path.
                    Example: /api → API instances, /images → Image processing instances.
          Both types of routing help optimize request distribution based on application requirements.
### 178. How does Sticky Sessions work in ELB:
          Sticky Sessions, also known as session affinity, ensure that requests from the same client are always directed to the same target for the duration of the session.
                    ALB uses Application Cookie Stickiness (custom app cookies) and Duration-Based Stickiness (AWS-generated cookies).
                    CLB uses Duration-Based Stickiness only.
                    NLB does not support Sticky Sessions.
          Use Case: Useful for applications that maintain user sessions in-memory, such as shopping carts.
### 179. What are Cross-Zone Load Balancing and its benefits:
           Cross-Zone Load Balancing allows an AWS Load Balancer to evenly distribute traffic across all instances in all AZs, instead of restricting traffic within a single AZ.
          Benefits:
                    Ensures balanced workload distribution across all instances.
                    Prevents uneven traffic distribution due to instance scaling differences.
                    Reduces the impact of an overloaded AZ.
                    ALB & CLB: Always enabled, free of cost.
                    NLB: Disabled by default, but can be enabled (incurs charges).
### 180. How do you secure an AWS Load Balancer:
          Use HTTPS (SSL/TLS) for encrypted communication.
          Implement AWS WAF to protect against common web attacks.
          Restrict access with Security Groups and NACLs.
          Enable Access Logging for monitoring requests.
          Use AWS Shield for DDoS protection.
          Leverage IAM roles and policies for restricted access.
## DAY16
### 181. How does Load Balancer handle sudden traffic spikes:
          AWS Load Balancers are designed to automatically scale to handle sudden traffic increases. However, the scaling speed depends on the load balancer type:
                    ALB: Uses a warm-up mechanism; scaling can take a few minutes.
                    NLB: Scales almost instantly due to its static IP nature.
                    CLB: Slower to scale compared to ALB and NLB.
          To handle traffic spikes effectively:
                    Use AWS Auto Scaling with EC2 instances.
                    Pre-warm the load balancer if expecting a high traffic event (for CLB).
                    Leverage AWS Global Accelerator for faster routing.
### 182. Can an ALB/NLB forward requests to multiple AWS accounts:
          Yes, ALB and NLB support cross-account target groups, which means they can route traffic to instances in different AWS accounts.
                    Helps in multi-account architectures.
                    Requires IAM permissions and resource sharing via AWS Resource Access Manager (RAM).
                    Security groups and IAM policies must be configured carefully to prevent unauthorized access.
### 183. What happens if all targets in a target group become unhealthy:
          If all targets in a target group fail health checks, the ELB stops routing traffic, causing application downtime. To prevent this:
                    Use Auto Scaling to replace unhealthy instances.
                    Configure multiple target groups across different Availability Zones.
                    Ensure proper grace periods for newly launched instances.
                    Implement failover mechanisms, such as Route 53 health checks.
### 184. How do you route traffic to an on-premises data center using AWS Load Balancer:
          To route traffic to an on-premises data center, you can:
                    Use NLB with IP targets, where on-prem servers are registered as IPs.
                    Use ALB with AWS Direct Connect or VPN to reach on-prem resources.
          Limitations:
                    Latency – Network round trips may introduce delays.
                    Security – Need proper firewall and IAM policies.
                    DNS Resolution – AWS-hosted apps may need Route 53 private hosted zones for smooth resolution.
### 185. How does AWS Load Balancer integrate with AWS Lambda:
          Yes, ALB directly integrates with AWS Lambda, allowing it to invoke Lambda functions without API Gateway.
                    ALB uses event-based invocation for serverless applications.
                    Supports multi-origin backend architectures (EC2 + Lambda in one load balancer).
                    Reduces the need for API Gateway for simple use cases
### 186. A Load Balancer is not distributing traffic evenly. What could be the reason:
          Possible Causes:
                    Cross-Zone Load Balancing is disabled (for NLB, this must be manually enabled).
                    Sticky Sessions (Session Affinity) is enabled, forcing users to a single backend instance.
                    Unequal instance health status, causing ELB to route requests to fewer instances.
                    Improper Auto Scaling settings, leading to imbalanced resource allocation.
          Troubleshooting Steps:
                    Check Target Group Health Checks (AWS Console → Target Groups).
                    Verify whether Cross-Zone Load Balancing is enabled.
                    Review CloudWatch Metrics to check request distribution.
                    Disable Sticky Sessions if load distribution is required.
### 187. You need to migrate from a Classic Load Balancer (CLB) to an Application Load Balancer (ALB). What is your approach:
          Migration Steps:
                    Create an ALB with a similar listener configuration.
                    Define Target Groups and associate EC2 instances.
                    Update DNS records (Route 53) to point to the ALB.
                    Modify Security Groups if needed.
                    Monitor traffic and phase out CLB after confirming ALB is fully operational.
          Challenges:
                    ALB does not support TCP-only traffic (use NLB instead).
                    Session stickiness behavior differs between CLB and ALB.
                    Some legacy applications may not support Layer 7 routing
### 188. How does AWS Load Balancer handle connection draining:
          Connection Draining (Deregistration Delay) ensures active requests are completed before terminating an instance.
                    ALB/NLB: Called Deregistration Delay, default 300 seconds.
                    CLB: Called Connection Draining, default 300 seconds, can be set to 0-3600 seconds.
                    Can be customized via ELB Target Group settings.
                    This prevents dropped connections when an instance is removed or replaced.
### 189. What is AWS Global Accelerator, and how does it compare to ELB:
          AWS Global Accelerator is a networking service that improves global application availability and performance by routing traffic to the nearest healthy AWS endpoint.
                    Comparison:
                    **Feature**	                    **ELB**	                    **Global Accelerator**
                    **Routing**	          Works at the regional level	          Works at the global level
                    **Protocol**	          HTTP, HTTPS, TCP, UDP	          TCP, UDP
                    **Latency Optimization**	          No	                    Yes (uses Anycast IPs)
                   ** Multi-Region Failover**	          No	                    Yes
                    **Best for**	          Load balancing within a region	Global traffic optimization
          You would use Global Accelerator for latency-sensitive applications with a global user base, whereas ELB is for distributing traffic within a single region.
### 190. How would you optimize cost when using AWS Load Balancer:
          Use Auto Scaling – Ensure instances scale only when needed.
          Choose the right ELB type – ALB for HTTP/HTTPS, NLB for TCP-heavy workloads.
          Enable Cross-Zone Load Balancing (only if needed) – NLB cross-zone incurs charges.
          Use AWS Savings Plans – Reserved Instances for predictable traffic patterns.
          Consider Global Accelerator – Reduces reliance on multiple regional ELBs for global traffic.
## DAY17
          What is Amazon RDS:
                    Amazon RDS (Relational Database Service) is a managed database service that makes it easy to set up, operate, and scale relational databases in the cloud. It automates time-consuming tasks like backups, patching, scaling, and replication, allowing users to focus on their applications. It supports multiple database engines such as MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, and Amazon Aurora.
### 191. Why would someone choose RDS over managing their own database:
          The key benefits of RDS include:
                    Managed Service – AWS handles administrative tasks like backups, patching, and scaling.
                    High Availability – Supports Multi-AZ deployments for automatic failover.
                    Scalability – Can be easily scaled vertically by increasing instance size or horizontally using Read Replicas.
                    Security – Provides encryption at rest and in transit, along with fine-grained access controls.
                    Performance Optimization – Offers automatic monitoring and tuning with Performance Insights and enhanced networking.
### 192. Can you list the database engines available in RDS:
          Yes, Amazon RDS supports the following database engines:
                    MySQL, PostgreSQL, MariaDB, Oracle, Microsoft SQL Server, Amazon Aurora (MySQL and PostgreSQL compatible)
### 193. Why would I choose RDS over running a database on EC2:
          RDS is managed, so AWS takes care of maintenance, backups, and scaling, while in EC2, we need to handle these manually.
          Automated backups and snapshots are available in RDS, whereas in EC2, we need to configure them ourselves.
          Multi-AZ deployments ensure high availability in RDS, whereas for EC2, we need to configure replication manually.
          Automatic patching in RDS, while in EC2, we are responsible for updates.
          Scaling is easier in RDS as it supports vertical and horizontal scaling with minimal downtime.
### 194. How is Amazon Aurora different from other RDS databases:
          Amazon Aurora is a cloud-native relational database designed for high performance and availability. Here’s how it differs:
                    Performance – Aurora provides up to 5x the performance of standard MySQL and 3x the performance of PostgreSQL.
                    Storage Auto-Scaling – Automatically scales up to 128 TB.
                    Replication – Aurora supports up to 15 read replicas, whereas standard RDS supports 5.
                    Failover – Aurora has faster failover times due to its distributed architecture.
                    Cost-Effective – Aurora charges only for the storage used, making it a cost-efficient option for large-scale applications.
### 195. Can you explain Multi-AZ deployment in RDS:
          Multi-AZ (Availability Zone) is a high availability feature in Amazon RDS. It automatically replicates data synchronously to a standby instance in a different Availability Zone. If the primary database fails, AWS automatically fails over to the standby, ensuring minimal downtime. This feature is mainly for high availability and disaster recovery rather than scaling read traffic.
### 196. What are Read Replicas, and how do they work:
          Read Replicas are used for scaling out read-heavy workloads. They create one or more copies of the primary database in the same or different AWS regions. These replicas asynchronously replicate data from the primary database and can be used for read queries. Unlike Multi-AZ, Read Replicas do not provide automatic failover; they are designed for improving performance by distributing read traffic.
### 197. What types of storage does Amazon RDS support:
          Amazon RDS supports three storage types:
                    General Purpose SSD (gp2/gp3) – Cost-effective and provides balanced performance.
                    Provisioned IOPS SSD (io1/io2) – High-performance storage optimized for transactional workloads.
                    Magnetic (Standard) – Deprecated in most cases, used for legacy applications.
### 198. What is the backup strategy in RDS:
          RDS provides automated backups and manual snapshots:
                    Automated Backups – Stores daily snapshots and transaction logs for point-in-time recovery, with a retention period of 1–35 days.
                    Manual Snapshots – User-initiated backups that are retained indefinitely unless manually deleted.
### 199. What security features does Amazon RDS provide:
          RDS provides multiple security features:
                    IAM authentication – Allows access control using AWS IAM.
                    VPC Isolation – Can deploy RDS inside a private subnet.
                    Encryption – Uses AWS KMS to encrypt data at rest and in transit.
                    Security Groups – Controls inbound and outbound traffic.
                    Automatic Patching – Keeps the database secure with the latest updates.
### 200. What happens when an RDS primary instance fails:
          In a Multi-AZ deployment, if the primary instance fails:
                    AWS automatically switches to the standby replica.
                    The DNS endpoint remains the same, so applications experience minimal downtime.
                    The failover process typically completes within a few minutes.
## DAY18
### 201. How does cross-region replication work:
          Yes, RDS supports cross-region Read Replicas, allowing you to replicate data asynchronously to another region for disaster recovery and global scalability
### 202. What are the steps for migrating a database to RDS:
          Choose a migration tool – AWS DMS (Database Migration Service) is recommended.
          Create an RDS instance – Set up the target database.
          Dump the data – Use mysqldump or pg_dump for manual migration.
          Use AWS DMS – For minimal downtime, AWS DMS supports continuous replication.
          Test the database – Validate performance and data integrity.
          Switch applications – Update applications to use the new RDS endpoint.
### 203. How can you reduce RDS costs:
          Use Reserved Instances – Provides significant discounts.
          Choose the right storage – Use gp3 instead of provisioned IOPS if performance needs are lower.
          Use Auto Scaling – Scale instances based on workload.
          Turn off non-production databases – Stop instances when not in use.
### 204. Your application is experiencing high latency when querying an Amazon RDS database. How do you troubleshoot and resolve this issue:
          To troubleshoot and resolve high latency in an RDS database, I would follow these steps:
                    Check CloudWatch Metrics – Look at CPU utilization, memory, and disk I/O to identify resource constraints.
                    Use Performance Insights – Identify slow-running queries and optimize them using indexes.
                    Check Read/Write Patterns – If read-heavy, use Read Replicas to offload traffic.
                    Review Connection Pooling – Ensure the application is not opening too many connections.
                    Adjust Instance Size – If the instance is under-provisioned, scale up to a larger instance type.
                    Check Query Execution Plans – Use EXPLAIN in MySQL/PostgreSQL to analyze queries.
                    Enable Caching – Use Amazon ElastiCache (Redis/Memcached) to reduce database load.
### 205. Your Amazon RDS instance is suddenly unavailable. How do you diagnose the issue and restore service:
          Check AWS Health Dashboard – Ensure there are no AWS-wide issues.
          Review CloudWatch Metrics – Check CPU, memory, and storage utilization.
          Check RDS Events – Look for maintenance activities, failovers, or connection issues.
          Verify Security Groups – Ensure security group rules allow inbound traffic.
          Multi-AZ Failover – If Multi-AZ is enabled, AWS should automatically failover to the standby instance.
          Restore from Backup – If the issue persists, restore from the latest automated backup or a manual snapshot.
          Check for Long-Running Queries – A locked or deadlocked query can cause service disruptions.
### 206. Your RDS instance is running out of storage. How do you handle this situation:
          Check Storage Metrics – Monitor storage consumption using CloudWatch.
          Enable Storage Auto Scaling – Allows automatic storage scaling when usage exceeds a threshold.
          Manually Increase Storage – Modify the instance to allocate more storage.
          Optimize Database Size – Remove unused indexes, archive old data, and optimize tables.
          Use Amazon S3 for Large Objects – Offload large files or logs to S3 instead of keeping them in the database.
### 207. Your application reports data corruption in an RDS database. How do you recover:
          Identify the Cause – Check logs and application errors to determine what led to corruption.
          Use Point-in-Time Recovery (PITR) – Restore to a time before the corruption occurred.
          Restore from Manual Snapshot – If PITR is not an option, restore from the latest snapshot.
          Verify Data Integrity – Use checksums or application-level validations.
          Prevent Future Issues – Implement Multi-AZ for failover protection and enable automated backups.
### 208. Your application suddenly starts failing to connect to the RDS database. How do you diagnose and fix it:
          Check RDS Endpoint – Ensure the application is using the correct endpoint.
          Verify Security Groups – Confirm inbound rules allow connections from the application.
          Check IAM Policies – If IAM authentication is used, verify correct permissions.
          Check Database Logs – Look for connection errors or failed authentication attempts.
          Restart the Instance – If necessary, restart the RDS instance to refresh the network settings.
          Monitor Connection Limits – Ensure the database has not exceeded the maximum allowed connections.
### 209. When would you use Multi-AZ, and when would you use Read Replicas:
          Use Multi-AZ when high availability and automatic failover are required. It ensures minimal downtime in case of failure.
          Use Read Replicas when scaling read-heavy workloads. They distribute read queries but do not provide automatic failover.
### 210. How does AWS apply maintenance and patches to RDS instances:
          AWS schedules maintenance windows for patching and upgrades.
          Minor version updates are automatically applied, while major versions require manual intervention.
          Maintenance can be postponed but must be applied eventually.
          AWS notifies users before maintenance, and downtime depends on the instance type and deployment model.
## DAY19
### 211. What is Amazon CloudWatch, and how does it differ from AWS CloudTrail:
          **Amazon CloudWatch** is a monitoring service that collects and tracks metrics, logs, and events from AWS resources and applications. It provides insights into performance, operational health, and resource utilization.
          **AWS CloudTrail**, on the other hand, records API activity and changes to AWS resources, providing a history of actions for security and auditing purposes. 
                    It records information like the identity of the caller, request time, source IP, and response
### 212. What are CloudWatch Alarms, and how do they work:
          CloudWatch Alarms monitor CloudWatch metrics and trigger automated actions based on threshold values. Actions include sending SNS notifications, Auto Scaling adjustments, or Lambda function invocations.
### 213. How do you create a custom metric in CloudWatch:
          You can use the AWS SDK, CLI, or API to publish custom metrics using PutMetricData. For example, an application can push a custom memory usage metric.
### 214. Your application’s EC2 instance CPU utilization is constantly at 90%. How would you set up an alert for this in CloudWatch:
          Navigate to the CloudWatch console and select Create Alarm.
          Choose the CPUUtilization metric for the EC2 instance.
          Set a threshold (e.g., >85% for 5 consecutive minutes).
          Define an action such as sending an SNS notification to administrators or triggering an Auto Scaling action.
### 215. How would you analyze high latency issues in an API hosted in AWS:
          Use CloudWatch Logs Insights to query API Gateway logs for high-latency requests.
          Check CloudWatch Metrics for API Gateway.
          Set up CloudWatch Alarms to detect spikes in latency.
          If using Lambda, check Duration and Throttles metrics.
### 216. A Lambda function is failing intermittently. How would you troubleshoot using CloudWatch:
          Check CloudWatch Logs for Lambda execution failures.
          Review the CloudWatch Metrics (Errors, Throttles, and Invocations).
          Use X-Ray Tracing to find performance bottlenecks.
          Set a CloudWatch Alarm on error count to notify the team.
### 217. How does CloudWatch Logs Insights help in real-time log analysis:
          CloudWatch Logs Insights allows you to query and analyze log data using a SQL-like syntax. You can filter logs, visualize trends, and find anomalies.
### 218. How do you forward CloudWatch Logs to an external monitoring tool like Splunk or ELK:
          Use CloudWatch Log Subscriptions with a Lambda function to process logs and forward them to Splunk, ELK, or another service.
### 219. How can you reduce CloudWatch logging costs:
          Set log retention policies to delete old logs.
          Use filters to log only essential events.
          Aggregate logs into S3 for long-term storage.
### 220. You suspect unauthorized access to your AWS account. How can you use CloudTrail to investigate:
          Use CloudTrail Event History to filter for suspicious API calls.
          Check for failed authentication attempts in IAM logs.
          Investigate API calls from unfamiliar IP addresses.
          If needed, set up GuardDuty to detect anomalies in API usage.
## DAY20
### 221. How would you track all actions taken by a specific IAM user:
          Use CloudTrail Event History and filter by the IAM user’s ARN.
          Enable CloudTrail Insights to detect unusual activity.
          Configure an SNS alert for any privileged actions.
### 222. An EC2 instance was terminated unexpectedly. How would you find out who did it:
          Open the CloudTrail console and search for TerminateInstances events.
          Identify the IAM user/role and timestamp of the action.
          Cross-check with CloudWatch Alarms or AWS Config to see if automated policies triggered the termination.
### 223. How can you secure CloudTrail logs from being tampered with:
          Enable S3 bucket logging and object versioning.
          Use S3 access policies to restrict modifications.
          Enable CloudTrail Log File Validation.
### 224. How can CloudTrail be integrated with SIEM solutions:
          Use AWS Lambda to process logs and forward them to Splunk or ELK.
          Utilize Amazon Kinesis Data Firehose to stream logs to a SIEM tool.
### 225. What is CloudTrail Insights, and how does it help in anomaly detection:
          CloudTrail Insights detects unusual API call patterns, such as spikes in failed authentication attempts or increased resource deletions.
### 226. How do you differentiate between a real user action and an automated process in CloudTrail logs:
          Check the user identity type in CloudTrail logs.
          Look at source IP (e.g., automated processes may originate from AWS services)
          Identify patterns of execution (e.g., periodic actions suggest automation)
### 227. How do you verify if the alarm actually transitioned to the ALARM state:
          Go to the CloudWatch console → Alarms section.
          Locate the specific alarm and check its History tab.
          Look for State Transition Events to see if it changed from OK → ALARM.
          If the state remains in OK or INSUFFICIENT_DATA, it means the condition was not met consistently.
### 228. Which specific CloudWatch metrics help identify whether the issue is CPU, disk, or network-related:
          CPU Issues: CPUUtilization
          Disk Bottlenecks: DiskReadOps, DiskWriteOps, DiskQueueLength
          Network Issues: NetworkIn, NetworkOut, NetworkPacketsIn, NetworkPacketsOut
          If the issue is I/O related, EBS metrics like VolumeQueueLength and VolumeIdleTime should be checked
### 229. How can you check if a Lambda function or external process is deleting logs prematurely:
          Open CloudTrail and search for DeleteLogStream or DeleteLogGroup events.
          Check IAM permissions of Lambda functions, automation scripts, or lifecycle policies that may be modifying logs.
          If using Kinesis Firehose or Lambda subscriptions, check whether logs are being forwarded elsewhere before deletion.
### 230. How can AWS GuardDuty complement CloudTrail in detecting malicious activities:
          GuardDuty analyzes CloudTrail logs to detect unusual API activities.
          It identifies threats like:
                    Unauthorized API calls
                    Excessive login failures
                    Data exfiltration attempts
          GuardDuty generates security findings that can be automatically acted upon using Lambda or AWS Security Hub.
## DAY21
### 231. What are the cost implications of enabling CloudTrail Data Events for all S3 buckets:
          Data Events incur additional charges per 100,000 recorded events.
          If tracking all objects across multiple buckets, the cost can increase significantly.
          A best practice is to enable Data Events only for specific high-value S3 buckets to reduce cost.
### 232. Can you list the different types of EBS volumes and when you would use each:
          General Purpose SSD (gp3, gp2) – Balances price and performance, good for general workloads like web servers and application hosting.
          Provisioned IOPS SSD (io2, io1) – High-performance storage with low latency, ideal for databases and critical applications.
          Throughput Optimized HDD (st1) – Designed for high-throughput workloads like big data and log processing.
          Cold HDD (sc1) – Low-cost storage for infrequent access, like backups and archives.
          Magnetic (standard, legacy) – Older generation, rarely used now.
          The choice depends on workload requirements. For example, for a high-performance database, I’d choose io2, but for a general application server, gp3 would be cost-effective.
### 233. Suppose you have an application running on an EC2 instance, and the EBS volume is running out of space. How would you resize the volume without downtime:
          AWS allows resizing EBS volumes dynamically using Elastic Volumes. Here’s how I’d do it without downtime:
                    Use the AWS Console or CLI to modify the volume size (aws ec2 modify-volume --volume-id <vol-id> --size <new-size>).
                    Monitor the state of the volume until it reflects the new size.
                    Inside the EC2 instance, use OS-specific commands:
                              For Linux: Use lsblk to check the new size, then growpart and resize2fs (for ext4) or xfs_growfs (for XFS).
                              For Windows: Use the Disk Management utility to extend the volume.
                    Since EBS supports online resizing, the process does not require downtime
### 234. What are the different ways to back up an EBS volume, and how do you ensure backup reliability:
          The most common way to back up an EBS volume is by creating EBS snapshots. A snapshot is an incremental backup stored in Amazon S3.
          Best practices for EBS snapshots:
                    Use AWS Backup to automate snapshot creation.
                    Follow a snapshot lifecycle policy to automatically delete old snapshots and save costs.
                    Use cross-region replication to store backups in another region for disaster recovery.
                    Ensure application consistency by pausing writes before taking snapshots (especially for databases).
          To take a manual backup:
                    aws ec2 create-snapshot --volume-id vol-1234567890abcdef --description "Backup before upgrade"
          For automated backups, I’d set up AWS Data Lifecycle Manager (DLM)
### 235.  Let's say you're working with sensitive data. How would you ensure your EBS volume is encrypted:
          AWS provides built-in encryption for EBS volumes using AWS Key Management Service (KMS). When creating a new volume, you can enable encryption, and AWS will handle encryption-at-rest, in-transit, and snapshot encryption.
          To encrypt an existing volume:
                    Take a snapshot of the existing unencrypted volume.
                    Create a new encrypted volume from the snapshot.
                    Attach the encrypted volume to the EC2 instance.
          Encryption considerations:
                    Performance impact: AWS offloads encryption, so there’s minimal performance overhead.
                    Cross-region security: If you copy an encrypted snapshot to another region, you need a KMS key in the destination region.
                    Access control: Use IAM policies to restrict KMS key usage.
### 236. Your company requires a highly available storage solution using EBS. How would you design it:
          EBS volumes are AZ-specific, so for high availability, I’d design a multi-AZ solution:
                    EBS Replication – Take frequent snapshots and copy them to another AZ. Use Amazon DLM for automation.
                    EFS (Elastic File System) – If shared storage is needed across multiple instances in different AZs.
                    RAID Configuration – For performance and redundancy:
                              RAID 1 (Mirroring): Provides redundancy, but at double the cost.
                              RAID 0 (Striping): Improves performance but has no redundancy.
                    Cross-region DR – Copy snapshots to another region for disaster recovery.
          For a database, I’d use RDS Multi-AZ instead of relying solely on EBS.
### 237. Your application is experiencing slow disk performance. What steps would you take to diagnose and resolve the issue:
          I’d follow these steps:
                    Check CloudWatch Metrics:
                              VolumeQueueLength: High values indicate IOPS saturation.
                              VolumeReadOps/WriteOps: Check if it matches the expected throughput.
                              BurstBalance: For gp2 volumes, depletion of burst credits can cause performance drops.
                    Analyze Instance Type:
                              Ensure the instance supports the expected EBS bandwidth. Some instance types limit throughput.
                    Upgrade the Volume:
                              If using gp2, consider switching to gp3 or io2 for better IOPS.
                              Use aws ec2 modify-volume to adjust the size or type.
                    Check OS-Level Issues:
                              Run iostat -xm 2 on Linux to check disk utilization.
                              Verify filesystem fragmentation and defragment if needed.
                    Use RAID 0:
                              Striping data across multiple EBS volumes can enhance performance.
### 238. Can you explain what Amazon EFS is and how it differs from EBS:
          Sure! Amazon Elastic File System (EFS) is a fully managed, scalable, and shared file storage system designed for Linux-based workloads. It allows multiple EC2 instances to access the same file system simultaneously, making it ideal for distributed applications.
          The key differences between EFS and EBS are:
                    EFS is a shared file system, whereas EBS is a block storage service attached to a single instance.
                    EFS scales automatically, while EBS requires manual resizing.
                    EFS supports multiple instances across different AZs, whereas EBS is tied to a single AZ.
                    EFS is best for shared storage needs, such as web servers, containerized applications, and big data workloads.
### 239. Suppose you have an EC2 instance and need to mount an EFS file system. How would you do it:
          To mount an EFS file system on an EC2 instance, I would follow these steps:
          Ensure NFS utilities are installed:
                    sudo yum install -y amazon-efs-utils  # For Amazon Linux
                    sudo apt-get install -y nfs-common    # For Ubuntu
          Mount the file system manually:
                    sudo mount -t efs fs-12345678:/ /mnt/efs
          To make it persistent after reboot, add the following entry to /etc/fstab:
                    fs-12345678:/ /mnt/efs efs defaults,_netdev 0 0
### 240. Your application needs high availability for shared storage. How would you configure Amazon EFS for this:
          EFS is designed for high availability by default because:
                    It is multi-AZ, meaning data is automatically replicated across multiple Availability Zones.
                    It has auto-scaling, so storage grows and shrinks as needed.
                    It provides Regional Resiliency, meaning all instances within a region can access the same file system.
          To enhance availability:
                    Deploy EC2 instances in multiple AZs.
                    Use Amazon EFS mount targets in each AZ.
                    Set up AWS Backup to protect against accidental deletions.
## DAY22
### 241. How does Amazon EFS handle performance scaling, and what are the best practices to optimize performance:
          EFS automatically scales based on demand, supporting both throughput and IOPS growth. It has two performance modes:
                    General Purpose Mode – Best for latency-sensitive applications.
                    Max I/O Mode – Designed for highly parallel workloads but with higher latency.
          To optimize EFS performance:
                    Use provisioned throughput if your workload requires consistent performance.
                    Distribute I/O operations across multiple files rather than a single large file.
                    Enable Elastic Throughput, which provides automatic scaling based on usage.
                    Use Amazon CloudWatch to monitor file system metrics and adjust throughput accordingly.
### 242. Security is a top priority for your application. How would you secure EFS data:
          To secure EFS, I would implement the following measures:
                    Encryption at Rest:
                              Enable AWS KMS-based encryption while creating the EFS file system.
                              Ensure encryption is enabled for all stored data.
                    Encryption in Transit:
                              Use TLS to encrypt data being transferred between EC2 instances and EFS.
                              Mount the file system with encryption enabled:
                                        sudo mount -t efs -o tls fs-12345678:/ /mnt/efs
                    Access Control:
                              Use IAM policies to restrict access to EFS.
                              Configure security groups and NFS client access rules to limit access.
                              Apply POSIX file permissions for fine-grained control over file access.
                    Network Security:
                              Ensure that the EFS file system is only accessible within the VPC.
                              Use AWS PrivateLink to restrict access further.
### 243. Your application is experiencing slow performance with EFS. How would you troubleshoot the issue:
          I’d follow these steps:
                    Check CloudWatch Metrics:
                              BurstCreditBalance: If it’s low, consider using provisioned throughput.
                              PercentIOLimit: If it’s high, your workload might be exceeding the file system’s capability.
                              TotalIOBytes: Helps determine if a single file or directory is the bottleneck.
                    Verify Mount Options:
                              Ensure the file system is mounted using amazon-efs-utils instead of standard NFS for better performance.
                              Use recommended mount options:
                                        sudo mount -t efs -o nfsvers=4.1,tls fs-12345678:/ /mnt/efs
                    Check Instance Network Throughput:
                              Since EFS performance depends on network bandwidth, ensure the EC2 instance type supports high network throughput.
                    Optimize File Access Patterns:
                              If many clients access the same file, consider breaking it into smaller files.
                              Use Max I/O mode for highly concurrent workloads.
### 244. How would you decide when to use EBS instead of instance store:
          I’d choose EBS when I need persistent storage that survives instance stops or terminations. It’s ideal for databases, application servers, and workloads requiring snapshots and backups.
          Instance store, on the other hand, is best when I need temporary, high-performance storage that’s automatically cleared when the instance stops. It’s useful for caching, temporary processing, or batch jobs where persistence isn’t necessary.
### 245. Is it possible to upgrade an existing gp2 volume to gp3 without downtime:
          Yes, AWS allows you to upgrade an existing gp2 volume to gp3 without downtime. The process is simple:
          Run the command:
                    aws ec2 modify-volume --volume-id vol-1234567890abcdef --volume-type gp3
          The volume modification happens in the background, and AWS ensures there’s no service interruption
          One advantage of gp3 over gp2 is that it provides consistent performance and allows you to configure IOPS and throughput independently.
### 246. Can you downsize an EBS volume? What happens if you try:
          No, EBS does not support reducing the size of a volume. Once you increase the size, you cannot shrink it directly.
          If I need to downsize a volume, I would:  
                    Take a snapshot of the current volume.
                    Create a new, smaller volume from the snapshot.
                    Attach the new volume to the instance and update the file system.
### 247. If you have an EBS snapshot, can you restore it in a different Availability Zone:
          Yes, EBS snapshots are stored in Amazon S3 and are region-wide, meaning I can restore them in any AZ within the same region.
                    Steps:
                    Create a new volume from the snapshot in the desired AZ:
                              aws ec2 create-volume --snapshot-id snap-1234567890abcdef --availability-zone us-east-1b
                    Attach the new volume to an instance in that AZ.
          If I need to move the snapshot to another region, I’d copy the snapshot first:
                    aws ec2 copy-snapshot --source-region us-east-1 --source-snapshot-id snap-1234567890abcdef --destination-region us-west-1
### 248. Can you share an encrypted EBS snapshot with another AWS account? If so, how:
          Yes, but there are additional steps for encrypted snapshots compared to unencrypted ones.
          I need to share the snapshot explicitly with another AWS account:
                    aws ec2 modify-snapshot-attribute --snapshot-id snap-1234567890abcdef --attribute createVolumePermission --operation-type add --account-id 123456789012
          Since it’s encrypted, I must also share the KMS key used for encryption.
          The receiving account must create a new volume from the shared snapshot before using it.
          Without sharing the KMS key, the other AWS account won’t be able to access the snapshot.
### 249. Is it possible to attach an EBS volume to multiple EC2 instances at the same time:
          By default, an EBS volume can only be attached to one EC2 instance at a time. However, there’s an exception:
                    EBS Multi-Attach (for io1/io2 volumes only): This allows an EBS volume to be attached to multiple instances in the same AZ.
                    All attached instances must run a cluster-aware file system (like Amazon FSx for Lustre or Oracle Cluster File System).
          For standard use cases, I’d use Amazon EFS instead of trying to share an EBS volume.
### 250. Suppose an application requires 10,000 IOPS. How would you configure EBS to support this:
          I would use an io2 volume, which allows provisioned IOPS:
                    io2 supports up to 1000 IOPS per GiB, so I’d create a volume with at least 10 GiB to meet the 10,000 IOPS requirement.
                    If I need additional performance, I could use RAID 0 striping across multiple volumes.
                    Monitor with CloudWatch and adjust the volume if necessary.
## DAY23
### 251. Can Windows EC2 instances use EFS:
          No, Amazon EFS only supports Linux-based instances because it uses the NFSv4 protocol, which Windows does not support natively.
          For Windows, I’d use:
                    Amazon FSx for Windows File Server, which provides SMB-based file shares.
                    EBS with Windows Storage Spaces, if local storage is required.
### 252. How does lifecycle management work in EFS, and can you customize it:
          EFS lifecycle management automatically moves files between Standard and Infrequent Access (IA) storage classes based on access patterns.
                    AWS provides preset age-based policies (e.g., move files to IA after 7, 14, 30, 60, or 90 days).
                    These policies are customizable, but they only apply to the entire file system, not individual files.
### 253. Can an EC2 instance in a different region access an EFS file system:
          No, EFS file systems are region-specific. However, I can use AWS DataSync or Cross-Region Replication to copy files to another region.
### 254. If the AWS region hosting an EFS file system fails, what happens:
          Since EFS is regional, it becomes unavailable if the region fails. To mitigate this:
                    Use AWS Backup to keep a copy in another region.
                    Replicate data using AWS DataSync to a second region.
### 255. What are burst credits in EFS, and what happens if they run out:
          EFS bursts performance based on burst credits. Every file system earns credits over time and uses them when it needs high throughput.
          If credits run out, the file system drops to its baseline throughput, which can slow down applications.
          To avoid this, I’d enable Provisioned Throughput for predictable performance.
### 256. Can you share an EFS file system with another AWS account:
          Yes, using resource-based IAM policies. I’d:
                    Attach a policy allowing access to another AWS account.
                    Ensure the security group and NFS settings allow connections.
### 257. If an application has a high-read, low-write workload, how do you optimize EFS:
          I’d:
                    Use EFS read replicas (if possible).      
                    Enable Elastic Throughput to handle variable workloads.
                    Implement caching with Amazon CloudFront or local caching on EC2.
### 258. Your EC2 instance crashed, and now the attached EBS volume is unresponsive. How do you recover the data:
          If the EBS volume is unresponsive, I’d take these recovery steps:
          1. Detach the EBS Volume:
                    aws ec2 detach-volume --volume-id vol-1234567890abcdef
          2. Attach the Volume to Another Healthy EC2 Instance:
                    Launch a new instance in the same AZ.
                    Attach the volume as a secondary device
          3. Check the File System:
                    List available volumes:
                              lsblk
                    Run a file system check and repair if needed:
                              sudo fsck -y /dev/xvdf
                    If using XFS, run:
                              sudo xfs_repair /dev/xvdf
          4. Mount and Recover Data:
                    Mount the volume to access files:
                              sudo mount /dev/xvdf /mnt/recovery
                    Copy important files to another location.
          5. Create a Snapshot for Future Protection:
                    aws ec2 create-snapshot --volume-id vol-1234567890abcdef --description "Backup before reattaching"
          6. Reattach the Volume to the Original Instance:
                    If the issue was instance-related, I would stop the instance and reattach the volume.
### 259. Your application is failing because the EBS volume is out of space. How do you increase its size without downtime:
          Expanding an EBS volume without downtime requires these steps:
                    1. Modify the EBS Volume:
                              aws ec2 modify-volume --volume-id vol-1234567890abcdef --size 100
                    The expansion happens in the background and does not cause downtime.
                    2. Wait for the Resize to Complete:
                              aws ec2 describe-volumes-modifications --volume-id vol-1234567890abcdef
                    3. Resize the File System:
                              If using ext4:
                                        sudo resize2fs /dev/xvdf
                              If using XFS:
                                        sudo xfs_growfs -d /
### 260. Your application team reports slow performance while reading and writing to an EFS file system. How do you troubleshoot:
          I would take these troubleshooting steps:
                    1. Check CloudWatch Metrics:
                              BurstCreditBalance: If low, the system is out of burst credits.
                              TotalIOBytes: Helps understand read/write patterns.
                    2. Use the Right Performance Mode:
                              Switch to Max I/O Mode if there are many parallel operations.
                    3. Check Mount Options:
                              Ensure correct NFS mount options:
                                        sudo mount -t efs -o nfsvers=4.1,tls fs-12345678:/ /mnt/efs
                    4. Consider Using Caching or CloudFront:
                              Implement Amazon CloudFront for static files.
                    5. Upgrade EC2 Instances for Higher Network Throughput.
## DAY24
### 261. Your ECS service, running on an EC2 launch type, is failing, and containers are not starting. How do you troubleshoot and resolve the issue:
          If an ECS service is failing on an EC2 launch type, I would take the following troubleshooting steps:

          1. Check ECS Service and Task Events:
                    Navigate to the ECS console → Services and check the Events tab to see failure messages.
                    Run:
                              aws ecs describe-services --cluster my-cluster --services my-service
                    This shows the status of running and pending tasks.
          2. Verify EC2 Instance Status:
                    Ensure the ECS container instances are running.
                    Run:
                              aws ecs list-container-instances --cluster my-cluster
                    Check if the instance has failed health checks or was terminated.
         3. Check IAM Permissions:
                    The ECS agent requires proper permissions (AmazonEC2ContainerServiceforEC2Role).
                    Verify if the ECS task execution role is correctly attached.
          4. Check CPU & Memory Usage:
                    If CPU or memory is exhausted, tasks may stop unexpectedly.
                    Run:
                              aws ecs describe-tasks --cluster my-cluster --tasks <task_id>
                    Increase CPU/memory limits if needed.
          5. Check Docker and ECS Agent Logs on EC2:
                    SSH into the instance and check logs:
                              sudo journalctl -u docker
                              sudo journalctl -u ecs
                    Restart the ECS agent:
                              sudo systemctl restart ecs
          6. Inspect Task Definition:
                    Ensure the container image is valid.
                    Verify networking settings, environment variables, and health checks.
### 262. You need to run an ECS service on private subnets without public internet access. How would you set up networking:
          To run ECS in private subnets:
          1. Ensure Subnets Are Private:
                    The route table should not have an Internet Gateway (IGW).
                    Instead, add a NAT Gateway to allow outbound internet traffic.
          2. Use AWS VPC Endpoints for Communication:
                    Create VPC endpoints for ECR, S3, and CloudWatch so ECS can pull images without internet access.
          3. Configure ECS Task Networking:
                    For Fargate:
                              {
                                "awsvpcConfiguration": {
                                  "subnets": ["subnet-abc123"],
                                  "securityGroups": ["sg-123456"],
                                  "assignPublicIp": "DISABLED"
                                }
                              }
                    For EC2, attach instances to a private subnet
### 263. You need to update an ECS service but must ensure zero downtime. How would you achieve this:
          To ensure zero downtime deployment when updating an ECS service, I would use the following deployment strategies:
                    1. Rolling Updates (Default):
                              Update the ECS task definition and service with a new image.
                              Set minimum healthy percent = 100% and maximum percent = 200% to ensure new tasks start before stopping old ones.
                              Run:
                                        aws ecs update-service --cluster my-cluster --service my-service --task-definition new-task
                    2. Blue/Green Deployment (Using AWS CodeDeploy):
                              Create a new ECS service (green) while keeping the existing service (blue) running.
                              Use AWS CodeDeploy to switch traffic gradually.
                              If issues occur, rollback without downtime.
                    3. Canary Deployment:
                              Deploy to a subset of tasks first, monitor for failures, then scale up.
                              Example: Deploy to 10% of tasks first, then 100%.
                    4. Load Balancer Health Checks:
                              Ensure the Target Group health check is set up properly so old tasks are removed only when the new ones are healthy.
                    5. Use Service Autoscaling:
                              If using ECS Fargate, configure auto-scaling to handle additional load during deployment.
### 264. Your ECS containers are being killed due to memory limits. What actions will you take:
          If tasks are failing due to out-of-memory (OOM) errors, I would:
                    1. Check Memory Usage Metrics in CloudWatch:
                    Monitor MemoryUtilization and MemoryReservation.
                    2. Increase Memory Limits in Task Definition:
                              Update the task definition with higher memory values:
                                        {
                                          "containerDefinitions": [
                                            {
                                              "name": "my-container",
                                              "memory": 512,
                                              "memoryReservation": 256
                                            }
                                          ]
                                        }
                              memory: Hard limit; the container gets killed if exceeded.
                              memoryReservation: Soft limit; tasks get more memory if available.
                    3. Enable ECS Task Auto-Scaling:
                              Use Service Auto Scaling to handle unexpected load spikes.
                    4. Optimize the Application:
                              Identify memory leaks in the application using logging and profiling tools.
                              Run lightweight applications or optimize background processes.
                    5. Use Spot Instances with Larger Memory (For EC2 Launch Type):
                              If running on EC2, choose instances with higher memory capacity.
### 265. Your ECS Fargate task is failing because it cannot pull the container image from Amazon ECR. What steps do you take:
           If an ECS Fargate task cannot pull an image, I would check:
                    1. Verify IAM Permissions for Task Execution Role:
                              The task execution role must have the following permissions:
                                        {
                                "Effect": "Allow",
                                "Action": [
                                  "ecr:GetDownloadUrlForLayer",
                                  "ecr:BatchGetImage",
                                  "ecr:GetAuthorizationToken"
                                ],
                                "Resource": "*"
                              }
                              Ensure the task is running with the correct execution role.
                    2. Check ECR Repository Policies:
                              If the image is in a private ECR repository, ensure the repository policy allows access.
                    3. Verify Image Tag and Name:
                              If the image tag was changed or removed, update the task definition with the correct tag.    
                              Run:
                                        aws ecr describe-images --repository-name my-repo
                    4. Confirm ECR Authentication:
                              If running manually, log in before pulling:
                                        aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <ECR_URI>
                    5. Check Network Settings:
                              If the ECR repository is in a different VPC or private subnet, configure VPC endpoints for ECR.
## DAY25
### 266. If the ECS agent on your EC2 instance is disconnected from the cluster, how do you fix it and re-register it:
          If an ECS agent is disconnected, the container instance will not report to the ECS cluster. To troubleshoot and re-register the ECS agent, I would follow these steps:
          1. Check the ECS Agent Status on the EC2 Instance:
                    SSH into the EC2 instance and check if the ECS agent is running:
                              sudo systemctl status ecs
                    If it’s stopped, restart it:
                              sudo systemctl restart ecs
          2. Ensure the ECS Agent is Running with the Correct Cluster Name:
                    Verify the cluster name in the ECS configuration file:
                              cat /etc/ecs/ecs.config
                    If the cluster name is missing or incorrect, update it:
                              echo "ECS_CLUSTER=my-cluster-name" | sudo tee -a /etc/ecs/ecs.config
                              sudo systemctl restart ecs
          3. Check IAM Role and Security Group
                    Ensure the EC2 instance IAM role has the required ECS permissions:
                              AmazonEC2ContainerServiceforEC2Role
                    Verify that outbound rules allow communication with the ECS control plane.
          4. Manually Re-register the ECS Agent (If Required):
                    If the agent is still not connecting, manually re-register the instance:
                              sudo amazon-linux-extras enable ecs
                              sudo yum install -y ecs-init
                              sudo systemctl enable ecs
                              sudo systemctl start ecs
          5. If the Instance is Stuck, Deregister and Re-add:
                    If an instance remains disconnected, deregister it:
                              aws ecs deregister-container-instance --cluster my-cluster --container-instance my-instance-id --force
### 267. How do you make sure ECS Fargate tasks can pull images from ECR without needing a manual login:
          In ECS Fargate, we use the task execution IAM role to grant the necessary permissions so that the task can pull images without manual authentication. Here’s how to ensure this:

          1. Attach the Correct IAM Role to the ECS Task:
                    The task execution role must have the following IAM policy attached:
                              {
                                "Effect": "Allow",
                                "Action": [
                                  "ecr:GetAuthorizationToken",
                                  "ecr:BatchCheckLayerAvailability",
                                  "ecr:GetDownloadUrlForLayer",
                                  "ecr:BatchGetImage"
                                ],
                                "Resource": "*"
                              }
                    This allows the ECS Fargate task to authenticate to ECR automatically.
          2. Ensure the Task Definition References the Correct Role:
                    In the task definition, specify the execution role:
                              "executionRoleArn": "arn:aws:iam::account-id:role/ecsTaskExecutionRole"
          3. Use Amazon ECR VPC Endpoints (For Private Subnets):
                    If the Fargate tasks run in private subnets, configure VPC endpoints for ECR to ensure seamless access.
### 268. How does AWS CodeDeploy automate blue/green deployments in ECS:
          AWS CodeDeploy enables blue/green deployments for ECS by creating a new version of the service (green environment) while keeping the existing service (blue environment) running. It then shifts traffic gradually, ensuring a zero-downtime rollout. Here’s how it works:
          1. CodeDeploy Creates a New Task Set (Green Deployment):
                    A new task set (green) is launched alongside the existing task set (blue).
                    This is done inside the same ECS service.
          2. Traffic Shifting Using a Load Balancer:
                    CodeDeploy reroutes traffic gradually from the blue (old) version to the green (new) version.
                    You can configure it to shift all traffic at once or in increments (canary deployments).
          3. Monitoring & Rollback:
                    You can set up CloudWatch alarms to monitor deployment success.
                    If the new version (green) fails health checks, CodeDeploy automatically rolls back to the old version (blue).
          4. Finalizing the Deployment:
                    Once the deployment succeeds, the old (blue) task set is terminated.
                    The new (green) version becomes the active service.
### 269. What is the difference between memory and memoryReservation in an ECS task definition:
          In ECS, both memory and memoryReservation control how much RAM a container gets, but they work differently:
                    1. memory (Hard Limit):
                              The maximum amount of memory the container can use.
                              If the container exceeds this limit, it gets killed (OOM error).
                              Example:
                                        "memory": 512
                              If a container needs 512MB but tries to use 600MB, it crashes.
                    2. memoryReservation (Soft Limit):
                              A soft limit that ECS tries to reserve for the container.
                              The container can exceed this limit if extra memory is available.
                              Example:
                              "memoryReservation": 256
                              If no memory is available, the container may get throttled but won’t be forcefully stopped.
                    Best Practice:
                    Set memoryReservation to a safe minimum and memory to an upper limit.
                    Example:
                    {
                      "memory": 1024,
                      "memoryReservation": 512
                    }
                    This ensures the container gets at least 512MB but won’t exceed 1GB.
### 270. Your ECS tasks are in a private subnet with no internet access. How can they pull images from ECR:
          Since private subnets don’t have direct internet access, ECS tasks cannot reach Amazon ECR without additional configurations. Here’s how to enable communication:
          1. Use AWS VPC Endpoints for ECR:
                    Create a VPC endpoint for ECR API and ECR Docker:
                              aws ec2 create-vpc-endpoint --vpc-id vpc-1234 --service-name com.amazonaws.us-east-1.ecr.api
                              aws ec2 create-vpc-endpoint --vpc-id vpc-1234 --service-name com.amazonaws.us-east-1.ecr.dkr
                    This allows ECS tasks to pull images from ECR without an internet gateway or NAT Gateway.
          2. Enable ECR IAM Permissions:
                    The ECS task execution role must have:
                              {
                                "Effect": "Allow",
                                "Action": [
                                  "ecr:GetAuthorizationToken",
                                  "ecr:BatchGetImage",
                                  "ecr:GetDownloadUrlForLayer"
                                ],
                                "Resource": "*"
                              }
          3. Check DNS Resolution in Private Subnet:
                    Ensure DNS resolution is enabled in the VPC settings so that ecr.amazonaws.com resolves correctly.
                    By using VPC endpoints, ECS tasks in private subnets can securely communicate with ECR without internet access.
## DAY26
### 271. Can you explain a scenario where using Amazon EKS would be more beneficial than running Kubernetes on EC2:
          Yes, let’s consider a scenario where a company is running multiple microservices that require high availability, scalability, and minimal operational overhead.
          If they deploy Kubernetes on EC2 instances (self-managed cluster), they would need to handle tasks like setting up the control plane, managing updates, handling scaling, ensuring high availability, and securing the cluster.
          By using Amazon EKS, AWS manages the Kubernetes control plane, including upgrades, patching, and scaling. This significantly reduces the operational burden. Additionally, EKS integrates natively with AWS services like IAM, VPC, CloudWatch, and ALB, making security and monitoring more seamless compared to a self-managed Kubernetes cluster.

### 272. How would you securely connect on-premise applications to an EKS cluster running in AWS:
          To securely connect on-premise applications to an EKS cluster, I would consider the following options:
          AWS Direct Connect:
                    Establish a dedicated Direct Connect link for low-latency and high-bandwidth access.
          Site-to-Site VPN:
                    Use an AWS VPN connection to securely connect on-prem resources to the VPC where EKS is deployed.
          Service Mesh (Istio or App Mesh):
                    Implement a service mesh for secure communication between on-prem services and EKS workloads.
          Ingress Controller with TLS:
                    Deploy AWS ALB or NGINX Ingress Controller with mutual TLS authentication.  
          IAM Role Assumptions & Fine-Grained Access Control:
                    Use IAM roles for service accounts (IRSA) to allow least-privilege access.
                    Restrict API access using Kubernetes RBAC policies.
          This setup ensures security, scalability, and minimal latency when connecting on-premise applications to an EKS cluster.
### 273. Your company needs a disaster recovery strategy for an EKS cluster. What approach would you take:
          For disaster recovery (DR) in an EKS cluster, I would implement the following strategies:
          Cluster Backup & Restore:
                    Regularly back up etcd data (for self-managed clusters) or use AWS Backup for EKS.
                    Use velero to back up Kubernetes resources and persistent volumes.
          Multi-Region Replication:
                    Deploy EKS clusters in multiple regions.
                    Use Cross-Region Replication (CRR) for S3 and EBS snapshots to replicate storage.
                    Implement AWS Global Accelerator for failover routing.
          Infrastructure as Code (IaC):
                    Use Terraform or CloudFormation to quickly spin up a new EKS cluster if needed.
          Database Replication:
                    Use Amazon RDS Multi-AZ or Amazon Aurora Global Database for data resilience.
          DNS Failover:
                    Configure Route 53 health checks to redirect traffic to a healthy region.
          By implementing these measures, I can ensure minimal downtime and quick recovery during a disaster.
### 274. Suppose your EKS cluster has performance issues. How would you troubleshoot and optimize it:
          If I notice performance degradation in an EKS cluster, I would follow these steps:
          Check Node Utilization:
                    Use kubectl top nodes and kubectl top pods to check CPU and memory utilization.
                    If nodes are under-provisioned, I would scale up the node group.
          Analyze Pod Scheduling Issues:
                    Use kubectl get events to check for scheduling failures.
                    If pods are pending, I would inspect if there are resource constraints or missing node taints.
          Monitor Network Latency:
                    Check Amazon VPC CNI metrics to identify pod-to-pod communication issues.
                    If necessary, optimize CIDR allocation and enable enhanced networking on nodes.
          Check Load Balancer Health:
                    Use AWS ALB/NLB logs to ensure traffic is being distributed evenly.
                    If an imbalance exists, I would adjust pod readiness/liveness probes.
          Enable Auto Scaling:
                    Use Cluster Autoscaler for scaling worker nodes dynamically.
                    Implement Horizontal Pod Autoscaler (HPA) based on CPU/memory utilization.
          By following these steps, I can identify bottlenecks and optimize the EKS cluster for better performance.
### 275. How would you design a multi-tenant architecture using Amazon EKS:
          In a multi-tenant environment, different teams or applications may share the same EKS cluster while maintaining isolation. There are a few strategies to achieve this:
          Namespace-Based Isolation:
                    Create separate namespaces for different tenants.
                    Apply RBAC (Role-Based Access Control) policies to restrict access to specific namespaces.
                    Use ResourceQuotas to limit resource consumption per namespace.
          Node Pool Isolation:
                    Use taints and tolerations to dedicate worker nodes to specific tenants.
                    Assign different AWS IAM roles to node groups for permission control.
          Separate VPCs or Network Policies:
                    Implement Kubernetes NetworkPolicies to restrict communication between different tenants.
                    Use AWS PrivateLink or service mesh (like Istio) to control cross-tenant traffic.
          This design ensures security, cost optimization, and scalability while allowing multiple tenants to coexist on the same EKS cluster
### 276. How would you handle networking configurations in an EKS cluster to ensure proper communication between microservices:
          To ensure proper communication between microservices in an EKS cluster, I would focus on:
          Networking Setup:
                    Use Amazon VPC CNI for native pod networking, allowing pods to get IP addresses from the VPC subnet.
                    Configure subnets properly (public/private) to ensure secure communication.
          Service Discovery & Load Balancing:
                    Use Kubernetes Services (ClusterIP, NodePort, LoadBalancer) for internal/external communication.
                    For advanced routing, leverage AWS ALB Ingress Controller or Nginx Ingress Controller.
          Network Security Controls:
          Implement Kubernetes Network Policies to restrict unwanted traffic between namespaces.
          Use Security Groups to allow traffic only from authorized sources.
          Service Mesh for Microservices Communication:
          Deploy Istio, Linkerd, or AWS App Mesh to handle service-to-service authentication, traffic routing, and observability.
          These strategies ensure smooth communication between microservices while maintaining security and scalability.
### 277. How would you ensure proper logging and monitoring for different tenants in a multi-tenant EKS cluster:
          To monitor and log multiple tenants in a multi-tenant EKS cluster, I would:
          Use AWS Native Monitoring Tools:
                    Amazon CloudWatch Logs & Metrics for centralized logging and performance monitoring.
                    Amazon CloudWatch Container Insights for pod-level monitoring.
          Implement Separate Logging for Each Tenant:
                    Use Fluentd, Fluent Bit, or AWS FireLens to forward logs to Amazon S3 or Amazon OpenSearch.
                    Apply namespace-based log segregation to track tenant-specific logs.
          Enable Kubernetes Auditing & Security Monitoring:
                    Enable Kubernetes audit logs to track user activities.
                    Use AWS GuardDuty for EKS to detect suspicious activities.
          Use Open-Source Monitoring Tools for Multi-Tenancy:
                    Deploy Prometheus & Grafana with multi-tenant dashboards.
                    Use Loki for log aggregation per tenant.
          This approach ensures that each tenant's logs and monitoring data are isolated, secure, and easy to analyze.
### 278. How would you reduce cold-start latency in an EKS cluster running event-driven applications:
          Cold-start latency in event-driven applications occurs when a pod needs to start from scratch due to scale-ups or resource allocation delays. To reduce this:
          Pre-Warm Pods Using HPA/KEDA:
                    Use Horizontal Pod Autoscaler (HPA) to keep a minimum number of warm pods running. 
                    Use KEDA (Kubernetes Event-Driven Autoscaler) for event-driven auto-scaling with lower latency.
          Enable Faster Node Provisioning:
                    Use Cluster Autoscaler with AWS EC2 Spot Instance Warm Pools to pre-scale worker nodes.
                    Opt for AWS Fargate for EKS, which removes cold-start overhead from EC2 instances.
          Optimize Container Start-up:
                    Reduce container image size using distroless images.
                    Enable lazy loading of dependencies to avoid unnecessary delays.
          Leverage Service Mesh for Caching & Traffic Routing:
                    Use Istio/App Mesh to route traffic to warm pods before scaling new ones.
          By implementing these techniques, I can significantly reduce cold-start time for event-driven workloads.
### 279. How would you test your disaster recovery plan to ensure it works effectively:
          To test a disaster recovery (DR) plan for an EKS cluster, I would follow a structured approach:
          Simulate Cluster Failure Scenarios:
                    Manually delete a node or introduce failures (kubectl delete node).
                    Simulate a region-wide outage using AWS Fault Injection Simulator (FIS).
          Verify Backup & Restore Procedures:
                    Ensure etcd backups (or Velero backups) are restorable.
                    Restore the cluster in a different AWS region and validate application recovery.
          Perform Load & Failover Testing:
                    Stress test applications using Chaos Engineering tools (e.g., LitmusChaos).
                    Ensure Route 53 DNS failover and AWS Global Accelerator function as expected.
          Validate Multi-Region Readiness:
                    Replicate databases (Amazon RDS/Aurora Global Database) and test cross-region failover.
                    Validate AWS ALB/NLB failover strategies.
          By conducting these tests regularly (quarterly or bi-annually), I can ensure a robust DR strategy for an EKS environment.
### 280. What are the security risks of using a public-facing Kubernetes API server, and how can you mitigate them:
          A public-facing Kubernetes API server is vulnerable to attacks, such as:
                    Brute force attacks
                    DDoS attacks
                    Unauthorized API access
          Mitigation Strategies:
                    Restrict API Access:
                              Use Private API Endpoint in EKS to keep the control plane internal.
                              Limit API server exposure using VPC peering or AWS PrivateLink.
                    Implement Strong Authentication & Authorization:
                              Use IAM roles for Kubernetes RBAC (eksctl create iamidentitymapping).       
                              Enable OIDC authentication with AWS Cognito or an identity provider.
                    Rate Limiting & Network Policies:
                              Apply AWS WAF to limit excessive API requests.
                              Use Kubernetes Network Policies to control access at the pod level.
                    Monitor & Audit API Calls:
                              Enable AWS CloudTrail logging for Kubernetes API events.
                              Use GuardDuty for EKS to detect unusual API activity.
          By implementing these measures, I can secure an EKS API server from unauthorized access and malicious attacks.
## DAY27
### 281. Your team is experiencing slow application performance on an Amazon ECS cluster running Fargate tasks. How would you diagnose and resolve the issue:
          To diagnose and resolve slow performance in an Amazon ECS cluster running on AWS Fargate, I would follow these steps:
          Check Task Resource Utilization:
                    Use CloudWatch Container Insights to analyze CPU and memory utilization.
                    If usage is near the limit, I would increase CPU and memory allocation per task.
          Investigate Task Placement & Scaling:
                    Ensure tasks are evenly distributed across Availability Zones.
                    If there are sudden traffic spikes, I would configure Application Auto Scaling to dynamically adjust the task count.
          Network Latency & Connectivity Checks:
                    Verify that the ECS tasks are using awsvpc networking mode for optimal performance.
                    Use VPC Flow Logs and AWS X-Ray to detect high latency between services.
          Storage & Database Bottlenecks:
                    If the app interacts with Amazon RDS, DynamoDB, or S3, I would check query performance and connection limits.
                    Enable RDS Performance Insights to optimize database queries.
          By following this approach, I can pinpoint the performance issue and implement an appropriate fix.
### 282. How would you handle a situation where an ECS task running on Fargate keeps restarting due to out-of-memory (OOM) errors:
          To fix OOM errors in Fargate ECS tasks:
                    Increase memory allocation in the task definition.
                    Optimize the application to use memory-efficient processing (e.g., reducing large in-memory caching).
                    Set ulimits (hard and soft memory limits) to prevent the container from using excessive resources.
                    Enable CloudWatch logging to check for memory leak patterns.
### 283. Your ECS service is not reaching the desired count of tasks. How would you debug and fix it:
          If the ECS service is not reaching the desired count of tasks, I would follow this approach:
          Check for Pending Tasks:
                    Run aws ecs describe-services to check the event messages in the service.
                    Use aws ecs list-tasks --desired-status PENDING to identify stuck tasks.
          Validate IAM Permissions:
                    Ensure the ECS task execution role has the required permissions to pull images and start containers.
          Check Cluster Capacity:
                    If using EC2 launch type, verify that there are enough available resources (CPU, memory, ENI limits) on the instances.
                    If using Fargate, check AWS service quotas to ensure Fargate is not hitting a soft limit.
          Task Definition Issues:
                    Check if the task definition image is valid and accessible.
                    Ensure environment variables and secrets are correctly configured.
          Once the root cause is identified, I would apply the appropriate fix and redeploy the service.
### 284. How would you handle an ECS deployment where tasks intermittently fail due to container health check failures:
          To address container health check failures in ECS:
                    Adjust health check parameters (grace period, interval, retries) in the ECS service definition.
                    Verify if the application inside the container starts slowly; if so, increase the health check grace period.
                    Use CloudWatch Logs and docker logs to debug application startup failures.
                    If using an ALB, verify that the target group health check settings align with the application’s readiness.
### 285. Your EKS cluster is experiencing high latency when handling API requests. How would you troubleshoot this:
          If my EKS cluster is experiencing high API request latency, I would:
          Check Cluster Load & Scaling:
                    Use kubectl top pods and kubectl top nodes to check CPU and memory usage.
                    Scale up nodes using Cluster Autoscaler if they are under-provisioned.
          Examine API Server Performance:
                    Use kubectl get events to see if there are any throttling or rate-limiting issues.
                    Enable CloudWatch Logs for EKS API Server and check slow response times.
          Investigate Network Latency:
                    Use VPC Flow Logs to see if requests are being delayed due to networking issues.
                    If using an NLB or ALB, check target response times in the AWS Load Balancer metrics.
          Check DNS Resolution Issues:
                    EKS heavily relies on CoreDNS; use kubectl logs -n kube-system -l k8s-app=kube-dns to check for DNS resolution failures.
                    Scale up CoreDNS if needed (kubectl scale deployment coredns --replicas=3).
          This approach helps pinpoint latency issues and resolve them efficiently.
### 286. If you suspect that API throttling is causing delays, how would you confirm and fix it:
          To check and fix API throttling in EKS:
                    Run kubectl get --raw "/api/v1/nodes?limit=1" to check for 429 (Too Many Requests) errors.
                    Check Amazon CloudWatch Metrics for API server request rates and throttling limits.
                    Increase the API server instance size if using Amazon EKS Managed Control Plane.
                    Implement Horizontal Pod Autoscaler (HPA) to distribute workloads more evenly.
### 287. Your team wants to migrate a monolithic application to Amazon EKS. What challenges would you anticipate, and how would you overcome them:
          Migrating a monolithic application to EKS poses several challenges:
          Breaking Down the Monolith:
                    I would first identify microservices within the monolithic application.
                    Gradually extract independent components and deploy them as separate Kubernetes services.
          Handling Stateful Dependencies:
                    If the monolith interacts with a database, I would migrate it to Amazon RDS or Amazon DynamoDB.
                    Use Persistent Volumes (Amazon EBS/EFS) for stateful workloads.
          Networking and Service Discovery:
                    Implement Kubernetes Services and Ingress Controllers to route traffic efficiently.
                    Consider using AWS App Mesh for better observability and service-to-service communication.
          Deployment Strategy:
                    I would use a blue-green or canary deployment strategy to minimize downtime.
                    Implement CI/CD pipelines with AWS CodePipeline & ArgoCD for automated rollouts.
          By taking a phased approach, I can ensure a smooth migration to EKS while reducing risks.
### 288. How would you ensure zero downtime during this migration:
          To ensure zero downtime during migration:
                    Use DNS-based traffic shifting (e.g., Route 53 weighted routing).
                    Deploy the new EKS-based system in parallel and gradually migrate traffic.
                    Implement rolling updates with Kubernetes Deployments to prevent disruptions.
                    Continuously monitor logs and rollback if necessary.
### 289. Your company is running ECS on EC2, but you want to migrate to EKS. What challenges would you anticipate, and how would you handle them:
          Migrating from ECS (EC2 launch type) to EKS presents challenges, including:
          Container Definition vs. Kubernetes YAML Conversion:
                    ECS uses task definitions, while EKS requires Kubernetes YAML manifests.  
                    I would use tools like Kompose to convert ECS task definitions into Kubernetes Deployment YAMLs.
          Networking Changes:
                    ECS (awsvpc mode) creates Elastic Network Interfaces (ENIs) per task.
                    EKS uses Kubernetes Services and CNI plugins for networking.
                    I would use Amazon VPC CNI for seamless networking integration.
          Storage Differences:
                    ECS primarily integrates with EFS, S3, and EBS for persistent storage.
                    EKS requires Persistent Volumes (PV) and Persistent Volume Claims (PVC).
                    I would migrate ECS storage solutions to Kubernetes-native persistent storage.
          Service Discovery & Load Balancing:
                    ECS uses AWS Service Discovery and ALB integration.
                    EKS relies on Kubernetes Ingress and CoreDNS.
                    I would configure an AWS ALB Ingress Controller to maintain external access.
          Monitoring & Logging:
                    ECS logs go to CloudWatch by default, while EKS requires FluentBit or CloudWatch Agent.
                    I would configure CloudWatch Container Insights for better visibility.
          By carefully planning the migration and using Kubernetes tools for AWS, I would ensure a smooth transition from ECS to EKS.
### 290. Your team is building an event-driven microservices architecture. Would you choose ECS or EKS? Why:
          For an event-driven microservices architecture, I would choose based on:
          Event Processing Needs:
                    If using Amazon EventBridge, SNS, SQS, ECS integrates natively with AWS event-driven services.
                    If requiring Kafka, RabbitMQ, or KNative eventing, EKS is the better option.
          Deployment Strategy:
                    ECS is ideal for simpler, managed event-driven services.
                    EKS provides custom event-driven scaling and Kubernetes-native event handling.
          Auto Scaling & Cost Optimization:
                    ECS with AWS Fargate scales on demand.
                    EKS supports KEDA (Kubernetes Event-Driven Autoscaler) for event-based scaling.
          Long-Term Flexibility:
                    If the architecture will remain AWS-focused, I would go with ECS.
                    If planning to expand to hybrid/multi-cloud, I would choose EKS.
          Final Decision:
                    For an AWS-native event-driven system, I would use ECS with EventBridge and Fargate.
                    If requiring Kubernetes-native event scaling, I would choose EKS with KEDA.
## DAY 28
### 291. What is AWS KMS, and how does it work:
          AWS Key Management Service (KMS) is a managed service that allows you to create, manage, and control cryptographic keys used for encryption and decryption. It integrates with various AWS services like S3, EBS, RDS, and Lambda to protect sensitive data. KMS supports both AWS-managed and customer-managed keys (CMKs), and it uses Hardware Security Modules (HSMs) to ensure secure key storage and access.
### 292. How do you enable automatic key rotation in AWS KMS, and why is it important:
           AWS KMS allows automatic key rotation for customer-managed symmetric keys. It can be enabled via the AWS Management Console, CLI, or SDK. When key rotation is enabled, AWS generates a new cryptographic key every year while retaining older versions for decryption purposes. This enhances security by reducing the exposure time of a single key.
### 293. Can you describe a real-time scenario where AWS KMS is essential:
          Consider a financial application that processes transactions and stores sensitive customer data. The application must comply with PCI-DSS regulations, which require strong encryption. AWS KMS can be used to encrypt customer PII data stored in S3, encrypt database records in RDS, and secure API keys used in AWS Lambda. This ensures that sensitive data remains protected, and access is controlled via IAM policies and KMS key policies
### 294. If an application is failing due to an AWS KMS access denied error, how would you troubleshoot it:
          First, I would check the IAM policies attached to the user or role accessing the KMS key to ensure they have the necessary kms:Encrypt and kms:Decrypt permissions. Next, I would review the key policy of the CMK to verify that the principal is allowed to use the key. Additionally, I would check AWS CloudTrail logs to see if there are any recent failed requests related to KMS operations. If it's an EC2 instance, I would ensure the instance profile has the correct permissions.
### 295. What is AWS Secrets Manager, and how does it differ from AWS Parameter Store:
          AWS Secrets Manager is a managed service that securely stores and manages secrets such as database credentials, API keys, and other sensitive information. It supports automatic secret rotation and integrates with AWS IAM for access control.
          AWS Systems Manager Parameter Store, on the other hand, is used for storing configuration data and secrets, but it lacks built-in rotation capabilities and is better suited for non-sensitive parameters. Secrets Manager is more suitable for managing highly sensitive information with automated lifecycle management.
### 296. A company is using AWS Secrets Manager but wants to automate secret rotation. How can they achieve this:
          AWS Secrets Manager supports automatic secret rotation by using AWS Lambda functions. When enabling rotation, you define a Lambda function that communicates with the database or service, generates a new secret, updates it in Secrets Manager, and updates the associated application. AWS provides pre-built rotation functions for services like RDS, or you can create a custom Lambda function for other secrets.
### 297. How would you securely store and access database credentials in an AWS environment:
          I would use AWS Secrets Manager to securely store the database credentials. The application would retrieve the credentials at runtime using AWS SDKs or IAM role-based authentication. I would also enable automatic rotation to update the credentials periodically without requiring manual intervention. IAM policies would be used to restrict access so only authorized services can retrieve the secrets.
### 298. How does AWS Secrets Manager help in preventing hardcoded secrets in an application:
          Hardcoding secrets in application code poses security risks, such as accidental exposure in source repositories or logs. AWS Secrets Manager eliminates this risk by storing secrets centrally and providing secure retrieval mechanisms. Applications can fetch secrets dynamically using AWS SDKs or API calls, ensuring that credentials are never exposed in code. Additionally, IAM-based access control ensures that only authorized entities can retrieve secrets.
### 299. How does AWS KMS ensure key security and prevent unauthorized access:
          AWS KMS ensures security by using AWS-managed Hardware Security Modules (HSMs) to store and process keys securely. It enforces access control through IAM policies and key policies, allowing only authorized users or roles to perform encryption and decryption. AWS CloudTrail logs every key usage event, enabling auditing and monitoring for unauthorized access attempts. Additionally, AWS KMS integrates with AWS Organizations and enables cross-account access controls to enhance security.
### 300. What happens to encrypted data when a key is rotated in AWS KMS:
          When a key is rotated in AWS KMS, a new cryptographic key is created, but the old key versions remain available for decryption. Any data encrypted with previous versions of the key can still be decrypted using the corresponding key version. New encryption operations will use the latest key version. AWS KMS ensures backward compatibility, so data remains accessible even after rotation.
