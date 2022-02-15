This exclusive notes helps you for your preparation for AWS Solutions Associate Architect exam. Of course, this doesn't cover details regarding each and every AWS Service out there but you will learn how to assess your preparedness for the AWS Certified Solutions Architect - Associate exam.
**Note**: _Thanks to aws skillsbuilder for the wonderful course which I've referred to prepare this notes_

#### 4 Modules

1. Design Resilient Architectures
2. Design High Performing Architectures
3. Design Secure Applications and Architectures
4. Design Cost-optimized Architectures

#### Module1: Multi-tier Solutions

#### 1. Design a multi-tier architecture solution

- Consider **access patterns** with regards to who and what needs access and how they will access the services and architectures

- Consider ways to **implement scaling**, how various services handle elasticity and methods to automated scaling needs

- Evaluate how **architecture requirements** will affect the selection of database, storage and compute services

#### 2. Design Highly available (HA) and/or Fault-tolerant (FT) architectures

- Highy available : Designing with **Minimal downtime**
- Fault Tolerant: **Zero downtime** and service interruption
- Determine amount of **resources needed**
- Determine which AWS services can be used to **improve reliability**
- Select **highly available configurations** to mitigate single points of failure and select appropriate disaster recovery strategies
- Understanding key performance indicators(KPIs) is essential

#### Disaster recovery objectives:

1. RTO (Recovery time objective)
2. RPO (Recovery point objective)

#### Disaster recovery strategies:

1.  Active/Passive - Backup and restore, pilot light and warm standby solutions
2.  Active/Active- Multi-site active/active deployment style

#### 3. Design Decoupling mechanisms using AWS services

- **Decoupling** refers to **components remaining autonomous and unaware of each other** as they complete their work as part of a larger system
  a) **Synchronous decoupling**- involves components that **must always be available for proper functionality**
  ex: **ELB** - managing instances across different availability zones
  b) **Asynchronous integration**- involves **communication between components through durable components**
  ex: **SQS** handling messages between instances

- Knowing **how to utilise decoupling services** will be incredibly important
  ex: ELB or Amazon Eventbridge

Services used to decouple application
a) SQS standard queue(doesn't care about ordering)
b) SNS(no guarantee of message delivery, ordering, no message persistence)
c) SQS FIFO queue(maintains order of messages)
d) Amazon Kinesis(realtime streaming data)

#### 4. Choose appropriate resilient storage

- Design strategy to **ensure the durability of data**
- Identify how **data service consistency** will affect operations
- Know how to implement a cross variety of architectures, including **hybrid or non-cloud-native applications**

- **EFS**: provides shared storage to multiple EC2 instances and manages them in parallel
- **Instance store**: is an ephemeral storage and can be attached to a single instance
- **EBS**: Preferred for systems that required frequent updates or storage of database application. A single EBS volume can't be mounted across multiple instances in a single availability zone

#### 5. Design Resilient Architectures:

- What **access paths** are available for instance or database management?
- **Block storage vs object storage**
- How do you **use AZs and Regions, failover mechanism and disaster recovery strategies** will be crucial to architecture design
- Understanding **services and feature usage** for decoupling and storage resources

#### Good reads:

[Decoupling message](https://docs.aws.amazon.com/prescriptive-guidance/latest/modernization-integrating-microservices/decouple-messaging.html)

[serverless](https://docs.aws.amazon.com/whitepapers/latest/serverless-multi-tier-architectures-api-gateway-lambda/introduction.html)

[decoupling serverless workloads](https://www.youtube.com/watch?v=VI79XQW4dIM)

[Disaster recovery and resiliency](https://docs.aws.amazon.com/efs/latest/ug/disaster-recovery-resiliency.html)

[well-architected](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc)

### Module 2: High-performing Architectures

#### 1. Identify elastic and scalable compute solutions for a workload

- AWS **Lambda**
  a) **Scalability and elasticity by default**
  b) **Adjust concurrency** to meet scaling needs
- Amazon **EC2**
  a) **Not inherently scalable and elastic**
  b) Use Amazon **EC2 Autoscaling to meet scaling needs**
- Know What Amazon **EC2 Instance type and family** will you choose
- Choose the appropriate architecture and **services that scale to meet performance requirements**
- Know What type of architecture would be **scalable solution for a specific workload?**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wekou36yod755fomb8om.png)

- Be ready to answer Architecture questions regarding the **usage of EC2,Lambda and ECS**
- Know the use cases, benefits and limitations of **AWS Compute services**
- Scaling metrics like **CPU Utilisation** or other metrics related to ELB like HealthyHostCount or SurgeQueueLength

#### 2. Select high-performing and scalable storage solutions for a workload

- EC2<->EBS Volume mapping
  Scale by
  a) Changing the volume size(Vertical scaling)
  b) Attaching more volumes (Horizontal scaling)
- EC2<->EFS File system mapping
  a) Scales automatically
- Determine which storage solution is the best fit based on future storage needs
- Know **general upper bounds for the capacity** of storage solutions
- Determine which solution would be the most appropriate for a situation based on performance
- Know the different **EBS Volume types and their performance implications**
- Familiarity with **S3**
  a) Basic API calls or CLI commands
  b) **Multipart uploads**
  c) Amazon **S3 Accelerator**
  d) **Caching with Amazon CloudFront**
- Consider using **multipart uploads for objects that are over 100MB**
- `aws s3 cp` (CLI command) automatically supports multipart upload and download based on file size

#### 3. Select high-performing networking solutions for a workload

- **Connect AWS cloud with On-premises data center** (through private connections) using
  a) AWS Managed VPN
  b) AWS Direct Connect
- **Connect multiple VPCs to a remote network** with the help of **AWS Transit Gateway**
- **AWS VPN CloudHub**: helps you **create a hub-and-spoke model** for connecting networks
- **Connectivity between VPCs**
  a) VPC Peering
  b) AWS Transit Gateway
  c) AWS PrivateLink
  d) AWS Managed VPN
- Connectivity to AWS for public services
- Understanding in-depth about **Route53 features** and develop solutions using it
- Know about **AWS Global Accelerator** that improves application network performance
- Consider **caching assets** closer to your end users by using **Amazon CloudFront**
- **Data transfer services**
  a) AWS DataSync
  b) AWS Snow Family
  c) AWS Transfer Family
  d) AWS Database Migration Service(AWS DMS)
- Depending on the **size of data**, **source and destination of data migration one service may be appropriate than other services**
- Know functional and performance **differences** between **data-transfer and migration services**
- **AWS PrivateLink** is best used when you have a client-server setup where you want to allow one or more consumer VPCs unidirectional access to a specific service(or set of instances) in the service-provider VPC
- How to establish a **AWS PrivateLink connection setup**?
  a) Create a LoadBalancer
  b) Create a service-consumer role in IAM
  c) Setup an endpoint connection in the shared services VPC and set it automatically accept
  d) Create consumer endpoints in each VPC that must access the shared VPC
  e) Point to Network Load Balancer in the shared services VPC
- **VPC Peering** has a limit of number of connections. One VPC can **accept up-to 125 peering connections**

#### 4. Choose high-performing database solutions for a workload

- Know if you **need a relational database or not?**
- Knowledge about **operations performed in Databases**
- If you need a single-digit millisecond response time then **DynamoDB** is the best choice
- Know the **differences**(performance and storage limitations) between **Amazon RDS and Amazon Aurora**
- Amazon **RDS Types**
  a) General Purpose SSD
  b) Provisioned IOPS SSD
  c) Magnetic
- Choose **appropriate scaling strategies** to meet your scaling needs
- DynamoDB automatically scales storage and you retain control over scaling throughput
- When to use one of the following?
  a) Provision throughput capacity
  b) Autoscaling for throughput
- To **Scale Amazon RDS**
  a) **Update the DB instance**(scale things like CPU usage)
  b) **Use Storage auto scaling**
  c) **Use Read replicas**
- Know how DB services scale up or down?
- Familiarity with the **Database caching features**
- Know **when to use Amazon ElasticCache for caching** and the impacts on performance
- Know what Database services are and the purpose they're built for
- DynamoDB stores the data in key-value pairs and DocumentDB doesn't support key-value

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/z1r1h68w1sewjje3uwt8.png)

#### 5. Design High Performing Architectures

- Solution Layers
  a) Compute
  b) Storage
  c) Database
  d) Networking
- If you're optimising for one of the below points, we need to know **which service to use**
  a) **Least amount of operational overhead**
  b) **Least amount of rework for a migration**
- Lift and shift to Amazon EC2 would require the least amount of effort
- Understanding the **Scaling mechanisms, Failover mechanisms** and **how to setup solutions** for the different **compute services**
- Understand **how Amazon EC2 auto scaling works** step by step and troubleshoot it
- Consider where the **AWS Service** you're using resides **in the AWS global infrastructure**
- Know how to facilitate **communication between applications across AZs or Regions**?
- Based on the **type of data** needs to be stored and the **performance requirements** will determine **what type of storage** to choose
- Know how to take and manage EBS snapshots
- Know when to **offload data requests to caches** to increase performance
- Know how the AWS global infrastructure is setup
- Understand **Amazon Route53** and underlying concepts like
  a) Different record types
  b) Different routing methods
  c) How Regional failover works?
- Know in-depth about **how to**
  a) **Create a VPC**
  b) **Create subnets**
  c) **Use networks ACLs**
  d) **Use Security groups**
  e) **Use route tables**
  f) **Use different gateways**
- **Networking services and features** to study:
  a) AWS Managed VPN
  b) AWS Direct Connect
  c) AWS Transit Gateway
  d) VPC peering
  e) AWS PrivateLink
  f) VPC endpoints

#### Good reads:

[Amazon EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)
[Using Amazon CloudWatch metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html)
[Overview of Amazon Web Services - Storage](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/storage-services.html)
[Amazon Virtual Private Cloud Connectivity Options - Introduction](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/introduction.html)
[How caching works with CloudFront edge locations](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cache-hit-ratio-explained.html)
[Overview of Amazon Web Services - Database](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/database.html)

### Module 3: Secure Applications

- Consider security at every stage, level and tier of your applications and architectures

#### 1. Design Secure access to AWS resources

- Know the details about AWS Identity & Access Management (IAM) users, groups and roles
- Techniques to **secure the root and other IAM users**
- Ways to **enable API access**
- How to **write and interpret policy documents**
- Also what are the ways in which the policies provide granularity with permissions?
- Understand the methods, services and tools that are available to help you **create traceability for access to AWS resources**
- How to ensure that root account follows the best practices for securely logging in ?
  a) **Enforce the use of MFA for the root user logins**
  b) **Enforce the use of complex passwords for member account root user logins**

#### 2. Design Secure application tiers

- Pay significant attention to use and functionality of security groups and network access control lists(network ACLs)
- Network segmentation
- Understand the strategies of when to use public and private subnets
- Common practices of the use of the subnets
- Understand routing mechanisms within a VPC
- Choose appropriate **AWS services to protect applications from external threats**
- Let us take a use case of a 3-tier architecture, How to ensure that VPC allows resources in web tier to be accessible from internet with only HTTPS protocol?
  a) Attach an internet gateway to VPC and Create public subnets for the web tier, Create private subnets for application and database tiers
  b) Create a web server security group that allows HTTPS requests from the internet. Create an application server security group that allows requests from web server security group only. Create a database cluster security group that allows TCP connections from the application security group on the database port only.

#### 3. Select appropriate data security options

- What methods are available within AWS to **secure your data both at rest and in transit?**
- How do various data management and storage services **handle data protection?**
- In-depth understanding about **Encryption and Key management**
- Encryption options in AWS?
- How are encryption keys handled?
- Will the use of encryption affect the performance?
- How would you handle root keys and will that method differ for your data keys?
- **Managed services that help secure, evaluate and audit the security of your data**
- Look into data security based on access patterns
- AWS Certificate Manager(used to store SSL keys)
- **AWS KMS keys** can be divided into two general **types**:
  a) **AWS managed key**
  b) **Customer managed key**
- An **AWS managed key** is created when you choose to **enable server-side encryption of an AWS resource** under the AWS managed key for that service for the first time.
- The AWS managed key is unique to your AWS account and the Region where it’s used. An AWS managed key can only be **used to protect resources within the specific AWS service for which it’s created**. It does not provide the level of granular control that a customer managed key provides.
- Provide security and durability in generating, storing and controlling cryptographic data keys
  a) Use AWS Key Management service(KMS) to solve AWSK KMS keys and data keys
  b) Use AWS KMS key policies to control access to KMS keys

#### 4. Design Secure Applications and Architectures:

- Who and what can access resources in your account and how that access is allowed and also the methods around creating and managing the access
- How to **protect web application and database tiers** and what firewalls you might use?
- How are **individual instances and resources should be protected** such as instances and interactions with the managed services that can be included as well. How are you protecting the network environment that contains these elements
- **VPCs** have option to **enable granular management of traffic flow and monitoring** within the network and these should be utilised collectively to provide compounding protection for your application
- Selecting appropriate data security options

#### Good reads

- [Security best practices in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Security groups for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)
- [Network ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html)
- [Route tables for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
- Data Protection
  a) [at Rest](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/protecting-data-at-rest.html)
  b [in Transit](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/protecting-data-in-transit.html)

### Module 4: Cost-optimized Architectures

#### 1. Identify Cost-effective storage solutions

- Understand **different storage solutions** that exist and know which one to use given a scenario
- Ways to **optimize Amazon EBS for cost**
  a) **Right-size EBS volumes**
  b) **Choose appropriate volume type** (how many IOPS you're using and compare it with how many IOPS you're paying for)
  c) Use services like **AWS Trusted Advisor** which gives recommendations when it find under utilised EBS volumes in your account
  d) **Delete old EBS snapshots (automatically)**. Know about the services AWS Data Lifecycle Manager and AWS Backup for solutions that automatically delete old EBS snapshots
- **Amazon S3 Storage tiers**( Know how to find a cost optimized solution based on the scenario)  
  a) S3 Standard - Highest for storage and Lowest cost for retrieval
  b) S3 Standard IA
  c) S3 Glacier
  d) S3 Glacier Deep Archive
- Understanding the **tradeoffs between each of the Storage classes based on storage cost and retrieval cost** is essential
- Ways to automate storage tiering for S3
- Use **Intelligent-tiering** that can be best used when access patterns change or for data with unknown access patterns
- Implement better governance for the lifecycle of Amazon EBS snapshots. **Automate lifecycle management of EBS Snapshots with least effort**
  a) **Create and schedule a backup plan with AWS Backup**
  b) **Use Amazon Data Lifecycle Manager(DLM)**
- **AWS Backup** is a backup service that
  a) **Automates the backup process for application data** across AWS services in AWS Cloud including Amazon EBS.
  b) Works to **automate the taking of EBS Snapshots**.
  c) Provides a central **place to configure and audit the AWS resources you want to backup**
  d) **Automates backup scheduling, set retention policies and monitor all recent backup and restore activity**
- **Amazon DLM** enables you to manage the lifecycle of your AWS resources through lifecycle policies which automate operations on specified resources. It supports EBS volumes and snapshots
- Copying EBS snapshots to Amazon S3 and then create lifecycle configurations in S3 bucket requires manual effort or create script that needs to be hosted somewhere
- **StepFunctions** can't manage EBS Snapshots

#### 2. Identify Cost-effective compute and database services

- **Amazon EC2 Pricing models**
  a) On-Demand Instances
  b) Reserved Instances(can be also be used for Amazon RDS DB instances)
  c) Dedicated Instances
  d) Spot Instances
  e) Savings Plans (Applicable for other compute services as well)

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wz034yh0jfaqiecv1vi4.png)

- Beyond the pricing models for EC2, consider **instance size and family for cost optimisation**
- Have **monitoring** in-place so that you can see how much utilisation your instances have, over time
- Right-sizing EC2 instances and RDS DB instances are a good way to optimize for cost
- Select appropriate **scaling strategies** based on scenario
- **Instead of Scaling-up the database instances, consider adding Read-replicas or caches to your Amazon RDS DB instances to absorb the read requests and offload the requests**. This will enable you to **optimize for both cost and performance**.
- By using **Storage auto scaling**, we can also **right-size storage for Amazon RDS db**
- Know about several scaling mechanisms available for both AWS DB and compute services
- Select the **correct Database service** based on your usecase and usage patterns
- **Use managed services when possible which remove the operational burden** of maintaining servers for tasks like running applications or managing databases. Because they operate at cloud scale, they can offer a lower cost per transaction or service. Some of the popular AWS Managed services are:
  a) **AWS Fargate for containers**
  b) **AWS Lambda for serverless compute**
  c) **Amazon DynamoDB for a database**
- The **most cost-effective solutions** that should meet requirements like scaling quickly, **microservices without operational overhead of managing infrastructure and to accommodate rapid changes in volumes of requests and protect against common DDos attacks**
  a) **Run microservices in AWS Lambda behind an Amazon API Gateway**
- **AWS Lambda** is
  a) Serverless computing service
  b) Fast built-in scaling
  c) Massive capability for scaling
  d) don't pay for idling resources
- **AWS API Gateway** is
  a) Serverless API Hosting service
  b) Fast built-in scaling
  c) Massive capability for scaling
  d) Throttle traffic to protect agains DDOS
  e) Protects at Layer 7 and Layer 3 against DDOS
  f) don't pay for idling resources

#### 3. Design Cost-optimized network architectures

- Remember that **data transfer and API calls can potentially incur costs**
- **S3 incurs costs for amount of data stored, API calls and also data transfer out of the bucket**
- The most cost effective thing to do when working with S3 is to front your S3 bucket with CloudFront
- **When and how to use CloudFront to optimize for costs and checkout the usecases beyond fronting an Amazon S3 bucket with the CloudFront distribution**
- Determine strategies to **reduce data transfer costs** within AWS
- Use of **VPC peering is more cost effective than that of AWS Transit Gateway**
- **Understand cost differences between usage of AWS Managed VPN and AWS Direct Connect**
- Solution with AWS Direct Connect would be more costly than using VPN Connection
- Direct Connect provides throughput and security
- Understand **cost implications of connectivity to resources**:
  a) SSH or RDP with bastion host
  b) AWS Systems Manager Session Manager
  c) Amazon EC2 Instance Connect
- Know **cost implications of NAT gateways or Transit gateways**
- **Cost effective and secure option to log into the EC2 instances in private subnet which have access to internet with NAT gateway**
  a) Configure **AWS Systems Manager Session Manager** for EC2 instance to enable login
- Session Manager enables to secure and auditable instance management without the need to open inbound ports, maintain bastion hosts or manage SSH keys
- There is no additional charge for accessing Amazon EC2 instances by using Session Manager
- Configure a bastion host in a public subnet to log into the EC2 instances in a private subnet would incur charges
- We can't establish an inbound connection to an instance with the help of NAT gateway

#### 4. Design Cost-optimized architectures

- Know the **ways for cost optimization** opportunities
- **For EC2, choose the appropriate pricing model for the usecase**
- **For Lambda, consider runtime and resource consumption**
- **For containers, you can save by having smaller, more lightweight containers and choosing the correct compute platform(EC2 or AWS Fargate) for your cluster**
- **For S3, use the appropriate storage tier for the usecase**
- **For EBS volumes or database backups, choose the appropriate volume type and automate the management of snapshot lifecycle**
- **For Database, choose the most-aligned database for the usecase. Consider caching mechanisms for cost savings (instead of scaling up or out) and also consider database design**
- **For networking, choose the correct connectivity service for the usecase. Know the configuration you need to make and the pricing models for each service**

#### Good reads:

- [Amazon S3 cost optimization for predictable and dynamic access patterns](https://aws.amazon.com/blogs/storage/amazon-s3-cost-optimization-for-predictable-and-dynamic-access-patterns/)
- [Managing your storage lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html)
- [Plan for Data Transfer](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/plan-for-data-transfer.html)
- [Analyzing your costs with AWS Cost Explorer](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-what-is.html)
