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
