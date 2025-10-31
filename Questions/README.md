╔════════════════════════════════════════════════════════════════════════╗
║               🌩️ AWS Interview Questions and Answers                   ║
║               Covers Basic → Intermediate → Advanced                   ║
║               + S3 + VPC + Database Sections                           ║
╚════════════════════════════════════════════════════════════════════════╝

---

### **Q1. What is AWS, and why is it so popular?**
AWS (Amazon Web Services) delivers scalable cloud computing solutions, providing on-demand infrastructure, tools, and services with worldwide accessibility, usage-based pricing, robust security, and a diverse array of offerings.

---

### **Q2. Define and explain the three basic types of cloud services and the AWS products based on them.**
The three primary categories of cloud services include Infrastructure as a Service (IaaS), Platform as a Service (PaaS), and Software as a Service (SaaS).  
AWS offerings consist of EC2 (IaaS), Elastic Beanstalk (PaaS), and AWS WorkDocs (SaaS).

---

### **Q3. What is Amazon EC2?**
Amazon EC2 provides flexible cloud computing, enabling users to deploy virtual servers and modify resources as required, paying solely for the computing time utilized.

---

### **Q4. What is Amazon S3?**
Amazon S3 is a service for object storage that allows data storage and access, offering capabilities such as:  
• Data durability  
• Lifecycle management  
• Replication across regions  

---

### **Q5. What is Amazon VPC?**
Amazon VPC enables users to establish isolated network environments in AWS by setting up IP ranges, subnets, and route tables for tailored and secure networking.

---

### **Q6. What is AWS Lambda?**
AWS Lambda executes code in reaction to events without the need for server administration, automatically scaling and accommodating multiple programming languages.

---

### **Q7. What is Elastic Beanstalk?**
Elastic Beanstalk streamlines deployment, scaling, and infrastructure management enabling developers to concentrate entirely on coding their applications.

---

### **Q8. What is Auto Scaling?**
Auto Scaling modifies AWS resource capacity in response to demand. It:  
• Guarantees application accessibility  
• Lowers expenses by adjusting resource levels as needed  
• Facilitates adaptive and forecasting scaling strategies  

---

### **Q9. What is Amazon RDS?**
Amazon RDS streamlines database administration by managing backups, updates, and scaling while supporting various database engines with high availability.

---

### **Q10. What is Amazon CloudFront?**
Amazon CloudFront provides content through a CDN, enhancing user experience and minimizing server load by utilizing a worldwide network.

---

### **Q11. What is the purpose of Amazon Route 53?**
Amazon Route 53 is a flexible DNS service crafted to direct end users to applications. It provides:  
• Domain registration  
• Health checks and monitoring  
• Load distribution across resources  

---

### **Q12. What are AWS Regions and Availability Zones?**
AWS Regions are geographical areas that contain several data centres, whereas Availability Zones are separate data centres located within a region. They ensure redundancy, fault tolerance, and high availability for applications.

---

### **Q13. What is the AWS Free Tier?**
The AWS Free Tier provides restricted no-cost access to services, such as EC2, S3 storage, and monthly Lambda requests.

---

### **Q14. What is AWS CloudWatch?**
AWS CloudWatch oversees resources and applications by gathering metrics, logs, and events to maintain performance, system wellness, and automation.

---

### **Q15. What is the difference between a Security Group and a Network ACL?**
A Security Group functions as a virtual firewall, managing both inbound and outbound traffic, whereas a Network ACL offers stateless traffic filtering at the subnet level.

---

### **Q16. What is Amazon DynamoDB?**
Amazon DynamoDB is a serverless NoSQL database cloud service fully managed by AWS. It scales to support high availability and low latency for applications like customer reservations.

---

### **Q17. What is Amazon SNS and its use case?**
Amazon SNS sends notifications between systems through SMS, email, or push notifications for instant alerts and application messaging.

---

### **Q18. What is Amazon ElastiCache?**
Amazon ElastiCache is a fully managed in-memory caching service that increases application performance by reducing latency and the load on databases.

---

### **Q19. What is Amazon Glacier used for?**
Amazon Glacier is a low-cost storage service with inexpensive retrieval costs for infrequently accessed data like backups and archives.

---

### **Q20. What is Amazon SWF?**
Amazon SWF (Simple Workflow Service) coordinates workflows for distributed applications, enabling the monitoring and management of tasks to create dependable, fault-tolerant processes.

---

## 🟢 **Intermediate AWS Interview Questions**

---

### **Q21. Explain the key components of AWS architecture.**
The AWS architecture consists of various components:  
• Compute (EC2, Lambda)  
• Storage (S3, EBS)  
• Database (RDS, DynamoDB)  
• Networking (VPC, Route 53)  
• Security (IAM, KMS)  
• Monitoring (CloudWatch)  
• Management tools (CloudFormation, Systems Manager)  

---

### **Q22. What are the different types of storage available in AWS?**
• Amazon S3 – Object storage  
• EBS – Block storage  
• Glacier – Archival storage  
• FSx and EFS – Managed file systems  

---

### **Q23. What is the difference between stopping and terminating an EC2 instance?**
Stopping retains data and configuration; terminating deletes the instance and attached storage (unless EBS).

---

### **Q24. How does Amazon S3 ensure data durability?**
S3 ensures **99.999999999% durability** by replicating data across multiple availability zones, checksums, and versioning.

---

### **Q25. What are the various load balancers provided by AWS?**
• Classic Load Balancer (CLB)  
• Application Load Balancer (ALB)  
• Network Load Balancer (NLB)  

---

### **Q26. How does Auto Scaling improve performance?**
Auto Scaling adjusts EC2 instances automatically according to traffic, ensuring performance while minimizing costs.

---

### **Q27. What is the difference between RDS Read Replicas and Multi-AZ?**
Read Replicas – Scale reads; Multi-AZ – ensures failover and high availability.

---

### **Q28. How can you secure an EC2 instance?**
Use security groups, IAM roles, encryption, and regular updates.

---

### **Q29. What are Amazon S3 lifecycle policies?**
They automate object transitions between storage classes or deletions after a set period.

---

### **Q30. What is the AWS Shared Responsibility Model?**
AWS manages the infrastructure; customers handle data, applications, and access control.

---

### **Q31. How do you implement disaster recovery in AWS?**
Use cross-region replication (S3), Multi-AZ RDS, and Route 53 failover.

---

### **Q32. What are the different types of EBS volumes?**
• gp3 – General-purpose SSD  
• io2 – High-performance SSD  
• st1 – Throughput-optimized HDD  
• sc1 – Cold HDD  

---

### **Q33. What is the difference between vertical and horizontal scaling in AWS?**
Vertical scaling → larger instance; Horizontal scaling → more instances.

---

### **Q34. What is AWS CloudFormation, and how does it work?**
Infrastructure-as-Code (IaC) service that uses templates to automate provisioning.

---

### **Q35. What is AWS OpsWorks?**
A configuration management tool using Chef/Puppet for managing infrastructure.

---

### **Q36. What is the purpose of IAM Roles?**
Provide temporary permissions for services (e.g., EC2, Lambda) instead of static credentials.

---

### **Q37. How do you create a VPC, and what are its components?**
Define CIDR range, subnets, route tables, gateways, and security components.

---

### **Q38. What is Amazon EMR, and when should it be used?**
A big data service using Hadoop/Spark for analytics, ML, and ETL.

---

### **Q39. What is AWS Config?**
A service that audits configuration changes and ensures compliance.

---

### **Q40. How do you optimize costs in AWS?**
Use Reserved/Spot Instances, Auto Scaling, Cost Explorer, and Trusted Advisor.

---

## 🔵 **Advanced AWS Interview Questions**

---

### **Q41. How do you automate EC2 backups using EBS snapshots?**
Use Data Lifecycle Manager (DLM) to schedule and manage automated backups.

---

### **Q42. What is the difference between instance store and EBS?**
Instance Store – Temporary; EBS – Persistent.

---

### **Q43. How do you improve database performance in RDS?**
Optimize queries, indexing, read replicas, and monitor via CloudWatch.

---

### **Q44. What is AWS Direct Connect, and how does it work?**
Provides dedicated private connections between on-premises and AWS.

---

### **Q45. How does Amazon Redshift support data warehousing?**
Uses columnar storage, compression, and parallel processing for large datasets.

---

### **Q46. What is AWS Lambda@Edge, and how does it differ from AWS Lambda?**
Executes Lambda functions at edge locations for lower latency.

---

### **Q47. How can you secure data at rest and in transit in AWS?**
Use encryption (KMS, SSE) and SSL/TLS for secure transfer.

---

### **Q48. What are the best practices for scaling in AWS?**
Use Auto Scaling, ELB, and stateless app design.

---

### **Q49. How does AWS implement CI/CD pipelines?**
With CodePipeline, CodeBuild, and CodeDeploy integrated with GitHub.

---

### **Q50. What is the role of AWS Transit Gateway?**
Connects multiple VPCs and on-prem networks centrally.

---

### **Q51. How do you troubleshoot latency issues in an AWS VPC?**
Use CloudWatch, VPC Flow Logs, and Reachability Analyzer.

---

### **Q52. What is AWS Trusted Advisor?**
Provides recommendations for cost, security, performance, and fault tolerance.

---

### **Q53. What are Global Tables in DynamoDB?**
Globally replicated DynamoDB tables for multi-region low-latency access.

---

### **Q54. What is Amazon Neptune, and what use cases is it suited for?**
Managed graph database for fraud detection, social networks, and recommendations.

---

### **Q55. How do you monitor and troubleshoot AWS Lambda performance?**
Use CloudWatch Logs, Metrics, and X-Ray for tracing.

---

### **Q56. What are S3 pre-signed URLs, and how are they used?**
Provide temporary access to private S3 objects securely.

---

### **Q57. How does Amazon Athena work?**
Run SQL queries directly on S3 data using a serverless model.

---

### **Q58. What is the AWS Service Catalog?**
Allows organizations to define and distribute approved AWS resource templates.

---

### **Q59. What is a blue-green deployment in AWS?**
Deploy updates using two environments (blue & green) for zero downtime.

---

### **Q60. How do you handle serverless application monitoring?**
Use CloudWatch, X-Ray, and custom metrics for end-to-end observability.

---

## 🟣 **AWS S3 Interview Questions**

---

### **Q61. What are the different storage classes in Amazon S3?**
Standard, Intelligent-Tiering, Glacier, and Deep Archive for varied use cases.

---

### **Q62. How does S3 handle versioning?**
Stores multiple versions of objects for recovery and protection.

---

### **Q63. What is the purpose of S3 Access Points?**
Simplify and control access for shared datasets with unique access policies.

---

### **Q64. What is cross-region replication in S3?**
Automatically replicates data to another AWS region for durability and compliance.

---

### **Q65. How can you secure an S3 bucket?**
Use bucket policies, IAM roles, encryption, MFA Delete, and block public access.

---

### **Q66. What is Amazon S3 Transfer Acceleration?**
Speeds up uploads using AWS global edge network.

---

### **Q67. What is the maximum size of an object in S3?**
Up to 5 TB (multipart upload for larger files).

---

### **Q68. How do lifecycle policies work in S3?**
Automate data transitions to lower-cost tiers or delete after a set time.

---

### **Q69. What is S3 Intelligent-Tiering?**
Automatically moves data between frequent/infrequent tiers to save costs.

---

### **Q70. How do you troubleshoot access-denied errors in S3?**
Check IAM policies, bucket policies, ACLs, and permissions.

---

## 🟡 **AWS VPC Interview Questions**

---

### **Q71. What are the key components of a VPC?**
Subnets, Route Tables, Internet Gateways, NAT Gateways, Security Groups, and ACLs.

---

### **Q72. How do subnets work in a VPC?**
Divide IP ranges into public and private sections for security and control.

---

### **Q73. What is the difference between a NAT Instance and a NAT Gateway?**
NAT Gateway is managed and scalable; NAT Instance requires manual maintenance.

---

### **Q74. What are VPC Peering connections?**
Connect two VPCs privately without public internet routing.

---

### **Q75. How does a VPC route table work?**
Controls how traffic is directed within and outside the VPC.

---

### **Q76. What is the purpose of VPC Flow Logs?**
Capture network traffic data for monitoring and troubleshooting.

---

### **Q77. How do security groups and network ACLs differ?**
Security groups are stateful; Network ACLs are stateless and work at subnet level.

---

### **Q78. What is a Transit Gateway in AWS?**
Connects multiple VPCs and networks centrally to simplify routing.

---

### **Q79. What is AWS Direct Connect, and how does it work with VPC?**
Provides a private, low-latency link from on-premises to AWS VPC.

---

### **Q80. How do you troubleshoot VPC connectivity issues?**
Check routing, ACLs, security groups, and use Flow Logs for diagnosis.

---

## 🔴 **AWS Database Interview Questions**

---

### **Q81. What is Amazon Aurora, and how does it differ from other RDS engines?**
High-performance, MySQL/PostgreSQL-compatible database with better scalability.

---

### **Q82. What is Amazon DynamoDB, and what are its use cases?**
NoSQL database for mobile, gaming, IoT, and real-time applications.

---

### **Q83. How does Multi-AZ improve database availability in RDS?**
Creates a standby replica in another AZ for automatic failover.

---

### **Q84. What is Amazon Redshift, and what are its key features?**
Data warehouse using columnar storage and parallel query processing.

---

### **Q85. What is ElastiCache, and how does it improve performance?**
Provides in-memory caching to reduce latency and DB load.

---

### **Q86. What is Amazon DocumentDB used for?**
Managed MongoDB-compatible NoSQL database for flexible data models.

---

### **Q87. How do you implement DynamoDB Streams?**
Enable streams to capture changes and process them with Lambda or Kinesis.

---

### **Q88. What is Amazon Neptune, and what is it used for?**
Graph database for connected data like social networks or fraud detection.

---

### **Q89. How do database snapshots work in AWS?**
Point-in-time backups that can be restored to recover lost data.

---

### **Q90. How can you monitor database performance in AWS?**
Use CloudWatch metrics, RDS Performance Insights, and Enhanced Monitoring.

---