## Design Resilient Architectures : 15 of 17 correct

### Question 22
You have taken over management of several instances in the company AWS environment. You want to quickly retrieve data about the instances such as instance ID, public keys, and public IP address. A URL command can be used to do this. What can you append to the URL  http://169.254.169.254/latest/ to retrieve this data?

#### Correct Answer 
meta-data/  
Rationale: Appending meta-data/ enables access to Amazon EC2 instance metadata, including instance ID, public keys, and public IP address. This is the standard, AWS-documented path.  

#### Incorrect Answers  
user-data/  
Rationale: Appending user-data/ returns custom launch-time configuration or scripts, not instance attributes.  

instance-demographic-data/  
Rationale: This option does not exist in AWS EC2 metadata or user data structure.  

Selected  
instance-data/  
Rationale: This is not a valid path for EC2 instance metadata or user data.  



### Question 52
You are the solutions architect for a website that uses MongoDB, a NoSQL database, on its backend. The database requires high, sequential read and write access to very large data sets on local storage. You need to migrate this database to AWS, host it on Amazon Elastic Compute Cloud (Amazon EC2), and attach Amazon Elastic Block Store (Amazon EBS) volumes. What Amazon EC2 instance and EBS configuration is best suited for I/O-intensive database workloads with sequential writes?

#### Correct Answer
Use storage optimized instances with provisioned IOPS SSD volumes.  
Rationale: Storage optimized Amazon EC2 instances, such as the I3 or I4 family, paired with provisioned IOPS SSD (io1/io2) Amazon EBS volumes, deliver sustained throughput and low-latency needed for sequential, high-I/O workloads.  

#### Incorrect Answers
Use compute optimized instances with general purpose SSD volumes.  
Rationale: Compute optimized instances focus on CPU, not storage I/O, and general-purpose SSD (gp3/gp2) volumes may not deliver consistent performance for demanding I/O operations.  

Selected  
Use memory optimized instances with provisioned IOPS SSD volumes.  
Rationale: Memory optimized instances are designed for workloads requiring high memory, not high disk throughput, and may not deliver the best storage performance despite fast EBS volumes.  

Use storage optimized instances with general purpose SSD volumes.  
Rationale: While storage optimized instances help, general purpose SSD volumes are not tailored for high-throughput, I/O-intensive applications, especially with sequential read/write patterns.  


## Design Secure Architectures : 10 of 20 correct
### Question 8
You are hired as a consultant by a small company to configure an AWS environment. You begin by working with the VPC and launching EC2 instances within it. You place the initial instances in a public subnet. Your next step is to create security groups. What is true about security groups?  

#### Correct Answers
Security groups operate at the instance level, not at the subnet level.  
Rationale: Security groups act as virtual firewalls that control inbound and outbound traffic at the instance level, not the subnet level. Each EC2 instance can have its own security groups, independent of the subnet it resides in. This is a fundamental distinction between security groups and Network ACLs (NACLs), which operate at the subnet level.  

Selected  
You can assign multiple security groups to a resource.  
Rationale: AWS allows you to assign multiple security groups to a single EC2 instance or other resources with network interfaces. This enables granular and flexible control of traffic rules by combining multiple sets of inbound and outbound rules.  

#### Incorrect Answers
Selected  
Security groups operate at the subnet level, not at the instance level.  
Rationale: Security groups do not operate at the subnet level; that is the role of Network ACLs (NACLs). Security groups are associated with individual instances or their network interfaces, not entire subnets.  

Security groups are stateless.  
Rationale: Security groups are stateful. For example, if an instance sends a request, the corresponding response traffic is allowed to reach the instance, even if there is no explicit inbound rule for it. Similarly, responses to allowed inbound traffic are permitted to leave the instance, regardless of the outbound security group rules.  


### Question 14
You are learning how to use role switching to access resources across multiple AWS accounts. To practice, you switch roles in the AWS Management Console from your primary account to a role in a second account. The role switch works, but when you try to view Amazon EC2 instances in the second account, you get an Access Denied error. You already verified that the trust relationship allows your primary account to assume the role. What should you check next to resolve the issue?  

#### Correct Answers  
Confirm that the target role has an identity-based policy that allows ec2:DescribeInstances.  
Rationale: After you assume a role, your effective permissions come from the target role’s policies (plus boundaries/Service Control Policies (SCPs)). A trust policy only lets you assume the role. It does not grant service permissions. To list instances in the console, the role needs ec2:DescribeInstances (the console issues that API call). If the role lacks that action, you will get Access Denied.  

#### Incorrect Answers  
Check whether the target role has permission for ec2:DescribeInstances.  
Rationale: The permissions of the source role do not apply after switching roles. Once the user assumes the target role, only the target role’s permissions govern what actions the user can perform. The source role’s permissions are irrelevant to the access granted in the target account.  

Switch roles using the AWS CLI instead of the console.  
Rationale: AWS supports role assumption both via the AWS Management Console and programmatically through the AWS CLI or SDKs. The AWS Management Console provides a built-in role switching feature that allows users to assume roles in other AWS accounts seamlessly. Therefore, it is not necessary to use the AWS CLI to assume roles for accessing resources across accounts. The permissions error after switching roles in the console is unrelated to the method of role assumption.  

Selected  
Check whether the source (primary-account) user or role has permission for ec2:DescribeInstances.  
Rationale: Once you switch roles, the source identity’s permissions no longer apply. Only the target role’s permissions matter, so checking the source permissions does not fix the issue.  



### Question 19
Your company is undergoing an annual audit, and auditors have requested AWS compliance reports and select online agreements. Which AWS service provides immediate access to this documentation?  

#### Correct Answers  
AWS Artifact  
Rationale: Enables direct, on-demand access to AWS compliance reports and agreements, helping organizations respond quickly to audit requests.  

#### Incorrect Answers  
AWS Audit Manager  
Rationale: Helps automate evidence collection for audits but does not offer access to AWS’s own compliance reports or legal agreements.  

Selected  
AWS Trusted Advisor  
Rationale: Provides guidance on cost optimization, security, and performance but does not supply audit or compliance documentation.  

Amazon Detective  
Rationale: Used for investigating security issues, not for retrieving compliance or audit documentation.  



### Question 23
Your company recently experienced a security breach that may have involved compromised IAM credentials and unexpected network activity. The CSO asks you to investigate the incident and determine which resources were affected and how the attacker moved through the environment. The solution must use behavioral analysis and machine learning to identify suspicious patterns based on historical activity. Which AWS service should you recommend?  

#### Correct Answers
Amazon Detective.  
Rationale: Amazon Detective is specifically designed to analyze, investigate, and quickly identify the root cause of potential security issues using behavioral analysis and machine learning. It automatically collects and correlates log data from AWS resources such as CloudTrail, VPC Flow Logs, and GuardDuty findings, building an interactive, unified view of resource and user activity over time. This enables efficient investigation of suspicious patterns, resource impact, and attacker movement within the environment, exactly meeting the requirements of the scenario.  

#### Incorrect Answers  
AWS Firewall Manager.  
Rationale: AWS Firewall Manager is a security management service that allows you to centrally configure and manage firewall rules across your accounts and applications in AWS Organizations. It is not used for root cause analysis of breaches using AI and ML.  

AWS Audit Manager.  
Rationale: AWS Audit Manager is used to map your compliance requirements to AWS usage data with prebuilt and custom frameworks and automated evidence collection. It is not used for root cause analysis of breaches using AI and ML.  

Selected  
Amazon Inspector.  
Rationale: Amazon Inspector is an automated vulnerability management service that continually scans AWS workloads for software vulnerabilities and unintended network exposure. It is not used for root cause analysis of breaches using AI and ML.  




### Question 25
Your team is building a microservices-based application deployed on Amazon Elastic Container Service (ECS). Each microservice requires access to different configuration values and secrets, such as API keys, database connection strings, and feature flags. You want a centralized, secure, and scalable solution to manage these configurations that supports versioning and easy updates without redeploying the services. Which AWS service is the best option to implement this requirement?  

#### Correct Answers  
AWS Systems Manager Parameter Store  
Rationale: Parameter Store provides centralized, hierarchical configuration management with versioning, IAM-based access control, and encrypted SecureString parameters (AWS Key Management Service (KMS)) that applications (ECS tasks) can fetch at runtime—enabling updates without redeploying. It can hold both general configuration values and some secrets. For secrets that require automatic rotation, pair Parameter Store with AWS Secrets Manager and reference those secrets from your configs.

#### Incorrect Answers
Selected  
AWS Secrets Manager  
Rationale: Secrets Manager is the best practice for sensitive secrets that need rotation (DB passwords, API keys). I is not a general-purpose configuration store for feature flags and broad app settings. Given a single service choice for both configs and some secrets with versioned, runtime retrieval, Parameter Store is the better overall fit. Secrets Manager can be used in addition for rotating secrets.  

Amazon S3 with encrypted configuration files  
Rationale: This is possible but not purpose-built. You would need to build your own retrieval, caching, version mapping, and access controls. It lacks built-in parameter versioning semantics and runtime update patterns tailored for application configuration management.  

AWS CloudFormation parameters  
Rationale: CloudFormation parameters are used during stack creation or updates and do not support dynamic configuration changes at runtime without redeployment. They are not designed for runtime configuration management or secrets storage.  





### Question 32
Your architecture consists of an Application Load Balancer (ALB) in front of an Auto Scaling group of EC2 instances, backed by an RDS database. Your security team reports cross-site scripting (XSS) and SQL injection (SQLi) attacks on the application. Which actions should you take to quickly mitigate these attacks?  

#### Correct Answers  
Selected  
Configure AWS WAF with rules to block SQL injection and cross-site scripting, and associate it with the ALB.  
Rationale: AWS WAF provides real-time, application-layer protection against SQLi and XSS attacks when associated with the ALB.  

Enable Amazon GuardDuty to detect suspicious activity.  
Rationale: Amazon GuardDuty detects suspicious activity and potential threats, helping identify attack sources quickly.  

#### Incorrect Answers
Selected  
Block offending IP addresses using Network ACLs (NACLs).  
Rationale: Network ACLs (NACLs) are stateless and operate at subnet level: ineffective for blocking Layer 7 web attacks.  

Use Amazon Inspector to detect vulnerabilities and manually block attacking IPs.  
Rationale: Amazon Inspector detects vulnerabilities but does not block attacks or IPs in real time.  

Implement AWS Shield Advanced to protect against application-layer attacks.  
Rationale: AWS Shield Advanced protects primarily against DDoS attacks, not specific application-layer attacks like SQLi or XSS.  

Restrict inbound HTTP traffic to the web tier only from specific IP addresses.  
Rationale: Restricting HTTP traffic by IP is not practical for public web applications and does not block SQLi or XSS attacks.  




### Question 35
You are designing a serverless application that needs to securely access multiple AWS services without embedding any static credentials in the code. What is the best practice for managing application credentials?

#### Correct Answers 
Use AWS Identity and Access Management (IAM) roles attached to the application runtime (for example, a Lambda execution role) to obtain short-lived credentials.  
Rationale: IAM roles provide automatically rotated, temporary credentials delivered by the runtime environment (AWS Lambda, Amazon Elastic Container Service (ECS), or Amazon Elastic Compute Cloud (EC2)). This approach removes the need for static access keys, aligns with the principle of least privilege, and is the AWS best practice for credential management in serverless architectures.

#### Incorrect Answers
Selected  
Store access keys in AWS Systems Manager Parameter Store with encryption enabled and fetch them at runtime.  
Rationale: Storing access keys in AWS Systems Manager Parameter Store with encryption is secure but still involves managing static credentials, which increases operational complexity and risk compared to using IAM roles with temporary credentials. It is better suited for configuration data or secrets that cannot be replaced by roles.  

Hardcode encrypted access keys in the application configuration and decrypt them using AWS KMS.  
Rationale: Hardcoding encrypted access keys in the application configuration poses a security risk, as keys can be exposed if the code is compromised. Decrypting with AWS Key Management Service (AWS KMS) adds protection but does not eliminate the fundamental issue of static credential management. This approach violates best practices.  

Use environment variables to pass static access keys to the application during deployment.  
Rationale: Passing static access keys via environment variables exposes credentials to risk, especially if environment variables are logged or accessed improperly. This method does not leverage AWS’s built-in temporary credential mechanisms and is discouraged for production workloads.  





### Question 49
A company is designing an authentication system for a new application. Users must be able to sign up and sign in with email and password. The application should support social identity providers such as Google and Facebook. Multi-factor authentication (MFA) needs to be optional but encouraged. Additionally, the application must store custom user attributes for each user. Which Amazon Cognito features should the solutions architect use to meet these requirements?  

#### Correct Answers
Use Cognito User Pools with a built-in user directory.  
Rationale: Cognito User Pools provide a built-in user directory supporting user sign-up and sign-in with email and password, which is essential for managing user authentication.  

Selected  
Enable social identity provider federation in Cognito User Pools.  
Rationale: Cognito User Pools support federation with social identity providers such as Google and Facebook, allowing users to sign in using these external accounts.  

Selected  
Configure optional MFA in Cognito User Pools.  
Rationale: Cognito User Pools allow configuration of multi-factor authentication (MFA) as optional, enabling the system to encourage but not enforce MFA for users.  

#### Incorrect Answers  
Selected  
Use Cognito Identity Pools to handle user sign-up and sign-in.  
Rationale: Cognito Identity Pools do not manage user sign-up or sign-in processes; they are designed to provide temporary AWS credentials for authorized users after authentication.  

Store custom user attributes in Cognito Identity Pools.  
Rationale: Cognito Identity Pools do not store or manage user attributes; management of user profile data and custom attributes is handled by Cognito User Pools.  

Use AWS Directory Service to manage user attributes and federation.  
Rationale: AWS Directory Service is primarily intended for integrating Microsoft Active Directory and is not typically used for managing social identity federation or custom user attributes in Cognito.  




### Question 55
You are a security analyst tasked with enabling IPv6 in a company’s AWS environment. Certain subnets must access internet endpoints using IPv6 addresses, but incoming internet traffic must be blocked by default. How should you configure the environment?  

#### Correct Answers
Add an IPv6 CIDR block to the VPC, assign IPv6 ranges to subnets, create and attach an egress-only internet gateway, and update route tables with a route having destination ::0 and target as the egress-only internet gateway.  
Rationale: This option correctly configures an egress-only internet gateway for IPv6, which allows outbound internet access while blocking inbound traffic by default. The route destination ::/0 is the IPv6 default route, and the target is properly set to the egress-only internet gateway, fulfilling the security and connectivity requirements.  

#### Incorrect Answers
Add an IPv6 CIDR block to the VPC, assign IPv6 ranges to subnets, create an IPv6 NAT Gateway, and update route tables with a route having destination 0.0.0.0/::0 and target as the NAT Gateway.  
Rationale: This option incorrectly uses an IPv6 NAT Gateway, which does not exist in AWS. Additionally, the route destination mixes IPv4 and IPv6 notation 0.0.0.0/::0, which is invalid, making this option incorrect.  

Selected  
Add an IPv6 CIDR block to the VPC, assign IPv6 ranges to subnets, create and attach an egress-only internet gateway, and update route tables with a route having destination 0.0.0.0/0 and target as the egress-only internet gateway.  
Rationale: This option uses an incorrect route destination 0.0.0.0/0, which is the IPv4 default route, not valid for IPv6 traffic. Although the egress-only internet gateway is correct for IPv6, the route destination must be ::/0 to route IPv6 traffic properly.  

Add an IPv6 CIDR block to the VPC, assign IPv6 ranges to subnets, create an internet gateway, and update route tables with a route having destination ::/0 and target as the internet gateway.  
Rationale: This option uses a standard internet gateway, which allows both inbound and outbound IPv6 traffic. It does not block incoming internet traffic by default, so it does not meet the security requirement to prevent inbound traffic.  




### Question 61
You manage a web application behind an AWS Application Load Balancer (ALB). The application must use HTTPS to meet compliance requirements. You have attached an SSL/TLS certificate from AWS Certificate Manager (ACM) to the ALB, but users report that they still receive browser warnings about an insecure connection. Which actions should you take to resolve this issue?  

#### Correct Answers  
Selected  
Verify that the ALB listener is configured to use HTTPS on port 443.  
Rationale: The ALB must have a listener explicitly configured for HTTPS on port 443 to terminate SSL/TLS. Without this, the ALB will not present the certificate properly, causing browser warnings.  

Ensure that the ACM certificate is issued and in the “In Use” state.  
Rationale: The ACM certificate must be fully issued and attached to the ALB listener. Certificates in pending validation or not attached correctly will cause browsers to warn of insecure connections.  

#### Incorrect Answers
Check that the security group attached to the ALB allows inbound traffic on port 80 only.  
Rationale: For HTTPS traffic, the security group must allow inbound traffic on port 443. Allowing only port 80 (HTTP) would prevent HTTPS connections, causing connection failures or warnings.  

Replace the ACM certificate with a self-signed certificate uploaded to IAM.  
Rationale: Self-signed certificates are not trusted by browsers and cause warnings. Using ACM certificates is best practice as they are trusted and managed by AWS.  

Selected  
Configure the target group to use HTTPS as the protocol to the backend instances.  
Rationale: SSL termination typically occurs at the ALB, which decrypts HTTPS and forwards requests to backend instances over HTTP. Configuring HTTPS on backend targets is optional and unrelated to browser warnings about the ALB’s certificate.  







## Design High-Performing Architectures : 11 of 16 correct

### Question 7
Your online store, hosted on Amazon Elastic Compute Cloud (EC2) instances in an Auto Scaling group behind an Application Load Balancer, is experiencing a traffic surge after national media coverage. A single Amazon Relational Database Service (RDS) instance is now a performance bottleneck. How can you scale the database to handle demand with minimal downtime?  

#### Correct Answers
Selected  
Add read replicas to the Amazon RDS database and update your web application to send read traffic to the read replicas.  
Rationale: Amazon RDS read replicas allow you to horizontally scale read operations by offloading read queries, increasing total throughput, and reducing load on the primary instance. This is a common solution for read-heavy workloads requiring more capacity.  

Migrate the database to Amazon Aurora Serverless.  
Rationale: Amazon Aurora Serverless auto-scales database capacity based on actual application demand. This can be a solution for handling unpredictable workloads and sudden spikes, though migration and application compatibility must be evaluated.  

#### Incorrect Answers
Selected  
Scale your Amazon RDS database out so that Multi-AZ is available.  
Rationale: Multi-AZ deployments improve availability and fault tolerance but do not help scale throughput. Standby instances in Multi-AZ cannot be used to serve additional read or write traffic.  

Refactor the database to Amazon DynamoDB and migrate the database to Amazon DynamoDB with Amazon DynamoDB Accelerator (DAX) enabled.  
Rationale: DynamoDB with DAX provides exceptional horizontal scalability for NoSQL patterns, but this requires substantial application refactoring and changes in data access, schema, and query logic, which is not a practical scale-out path for an online relational database under urgent demand.  




### Question 30
You are designing a global e-commerce application hosted in multiple AWS Regions. The application must route customers to the nearest active Region to minimize latency and maximize performance. If a Region becomes unavailable, the system must automatically redirect traffic to the next closest healthy Region without requiring manual intervention. What should you do to meet these requirements?  

#### Correct Answers
Use Amazon Route 53 with a latency-based routing policy and configure health checks for each endpoint.  
Rationale: Route 53 latency-based routing directs users to the closest healthy Region and automatically reroutes on failure.  

#### Incorrect Answers
Use an Application Load Balancer with cross-Region targets and set listener rules based on IP geolocation.  
Rationale: ALBs do not support cross-Region targets, and listener rules cannot route based on geolocation.  

Selected  
Use AWS Global Accelerator with static IPs to route traffic using geolocation routing.  
Rationale: Global Accelerator uses performance-based routing, not geolocation, and requires additional configuration for failover behavior.  

Use Amazon CloudFront with a regional edge cache and origin failover pointing to a single Region.  
Rationale: A single Region origin with failover does not provide true multi-Region high availability and reduces resilience.  



### Question 38
A video analytics company processes telemetry data from millions of smart cameras deployed across multiple cities. The devices send semi-structured JSON data continuously. The company needs to ingest this data, transform it near real-time, and store it in Amazon Simple Storage Service (Amazon S3) for long-term analytics. The solution must scale automatically with traffic, offer high throughput, and require minimal operational effort. What should you implement to meet these requirements?  

#### Correct Answers
Use Amazon Kinesis Data Firehose to ingest and transform the data before delivering it to Amazon S3.  
Rationale: Kinesis Data Firehose handles scalable ingestion and supports near-real-time transformation with minimal management overhead.  

#### Incorrect Answers
Selected  
Use AWS Glue to ingest the data directly from the devices, apply transformation, and write results to Amazon S3.  
Rationale: AWS Glue is not suitable for real-time ingestion from devices; it is a batch ETL service and lacks near-real-time capabilities.  

Use Amazon S3 Transfer Acceleration to receive data directly into S3 and run AWS Lambda on the objects for transformation.  
Rationale: S3 Transfer Acceleration is designed to speed up uploads, not provide a transformation pipeline for streaming data ingestion.  

Use Amazon Simple Queue Service (Amazon SQS) with a consumer application running on Amazon EC2 to process and store the data.  
Rationale: SQS with EC2 lacks automatic scaling and near-real-time processing, increasing complexity and reducing fault tolerance.  



### Question 45
You are the database administrator for a financial services company running a legacy Amazon Relational Database Service (Amazon RDS) for MySQL. The database suffers from connection timeouts and slow read queries during peak hours, and availability must improve without redesigning the application. What actions should you take?  

#### Correct Answers
Enable Amazon RDS Multi-Availability Zone (Multi-AZ) deployment.  
Rationale: Multi-AZ deployments provide synchronous replication and automatic failover, minimizing downtime during maintenance or failures without needing application changes.  

Selected  
Create Amazon RDS Read Replicas.  
Rationale: Read Replicas distribute read traffic away from the primary instance, reducing query latency and connection timeouts during peak periods without impacting writes or requiring application redesign.  

#### Incorrect Answers
Scale up the Amazon RDS instance size.  
Rationale: Vertical scaling alone may temporarily improve performance but does not address read scalability or availability and may not resolve connection issues under load.  

Migrate the database to Amazon DynamoDB.  
Rationale: Migrating to Amazon DynamoDB requires significant application redesign due to different data models and APIs, which violates the requirement to avoid redesign.  

Selected  
Introduce Amazon ElastiCache in front of the database for query caching.  
Rationale: Query caching can improve read latency but does not provide fault tolerance or failover capabilities, leaving availability issues unresolved.  




### Question 60
You work for a travel reservation company that manages hotel and flight bookings globally. The company needs to migrate its on-premises relational booking database to AWS. The workload experiences predictable read/write operations with occasional spikes during holidays and sales. Management requires a highly available solution with minimal administrative overhead and optimized performance. What is the most suitable Amazon database service for this scenario?  

#### Correct Answers
Use Amazon Aurora with Aurora Replicas in multiple Availability Zones.  
Rationale: Provides high availability, automated scaling, and performance optimization with minimal administration.  

#### Incorrect Answers
Selected  
Use Amazon RDS on a single Availability Zone with provisioned instances.  
Rationale: Does not provide high availability; a single Availability Zone setup is a single point of failure.  

Use Amazon RDS with Multi-AZ deployments and manual backups.  
Rationale: Although highly available, manual backups introduce unnecessary administration and do not improve performance.  

Use Amazon DynamoDB with on-demand capacity mode.  
Rationale: DynamoDB is not a relational database and would require application refactoring to support its data model.  


## Design Cost-Optimized Architectures 8 of 12 correct

### Question 1
You are a systems administrator for a manufacturing company exploring ways to connect your on-premises data center to Amazon Web Services (AWS). After evaluating technologies such as AWS Direct Connect and AWS Virtual Private Network (AWS VPN), you decide to implement a VPN connection for hybrid cloud integration. What features and advantages can an AWS VPN connection provide?  

#### Correct Answers
Selected  
It provides a connection between an on-premises network and an Amazon Virtual Private Cloud (VPC), using a secure and private connection with IPsec and TLS.  
Rationale: AWS VPN enables secure, encrypted tunnels between your data center and Amazon VPC using Internet Protocol Security (IPsec) and, for client VPN, Transport Layer Security (TLS), supporting data privacy over public networks.  

It provides a cost-effective, private network connection that uses your existing internet connectivity.  
Rationale: AWS VPN leverages your company's current public internet access, avoiding the cost and complexity of dedicated leased lines while providing private, encrypted connectivity between AWS and on-premises resources.  

#### Incorrect Answers
Selected  
It provides a private, dedicated network connection between an on-premises network and the Amazon Virtual Private Cloud (VPC).  
Rationale: AWS Direct Connect, not VPN, provides a dedicated, private physical link. Site-to-Site VPN uses encrypted connectivity over the public internet, not a dedicated line.  

Data transfer costs across an AWS VPN are completely free.  
Rationale: AWS VPN has hourly connection fees and data transfer charges apply. Data transferred out of AWS is not free over VPN; only the first 100 GB per month are free for some tiers.  




### Question 13
You are a cloud architect at a mobile gaming company preparing to launch a new game. The backend must be fully serverless to reduce costs as much as possible. Which architecture offers the most cost-effective serverless design?  

#### Correct Answers
Use Amazon API Gateway with AWS Lambda, Amazon DynamoDB, and Amazon Simple Storage Service (S3).  
Rationale: This option represents a fully serverless architecture with all components following a pay-per-use pricing model. Amazon API Gateway serves requests without provisioning servers, AWS Lambda handles compute dynamically, Amazon DynamoDB is a serverless NoSQL database, and Amazon S3 provides durable, cost-effective object storage. This minimizes idle and fixed costs.  

#### Incorrect Answers
Use Amazon API Gateway with Amazon Elastic Compute Cloud (Amazon EC2), Amazon DynamoDB, and Amazon Simple Storage Service (S3).  
Rationale: Introducing Amazon EC2 breaks the serverless paradigm by requiring provisioned servers, resulting in fixed costs even during idle times. It increases operational overhead and deviates from the cost minimization goal.  

Selected  
Use Amazon API Gateway with AWS Lambda, Amazon Relational Database Service (Amazon RDS), and Amazon Simple Storage Service (S3).  
Rationale: RDS is managed, but not serverless. You size and pay for database instances continuously (plus storage/IO), so it does not scale to zero and adds ongoing cost, violating the fully serverless, cost-minimizing goal. (Aurora Serverless is a separate service/engine, not generic RDS, and still maintains minimum capacity.)

Use Amazon API Gateway with AWS Lambda, Amazon DynamoDB, Amazon EC2, and Amazon Elastic File System (Amazon EFS).  
Rationale: The addition of Amazon EC2 and Amazon EFS introduces server-based components, adding fixed costs and operational complexity. Both services are not serverless, thus violating the requirement for a fully serverless, cost-optimized architecture.




### Question 31
Your company is expanding its AWS footprint while maintaining an on-premises data center. To reduce costs, the team has begun migrating services to AWS across multiple accounts, each with its own VPC. You already have a single AWS Direct Connect connection. What is the most cost-effective way to provide dedicated, scalable connectivity between your data center and all AWS accounts?  

#### Correct Answers
Create a new AWS Direct Connect gateway and set this up with the existing Direct Connect connection. Set up a transit gateway between the AWS accounts and connect the transit gateway to the Direct Connect gateway.  
Rationale: Using a Direct Connect gateway with a transit gateway enables centralized management of a single high-capacity link across multiple accounts and VPCs. This approach avoids multiple dedicated circuits, reduces operational cost, and scales as more VPCs or accounts are added.  

#### Incorrect Answers
Use a VPN concentrator to connect the AWS accounts back to the on-premises data center.  
Rationale: VPN is a lower cost but less performant option, using the public internet for connectivity. It does not provide the dedicated, high-performance, and predictable bandwidth of Direct Connect, nor is it optimal for production workloads requiring consistent performance.  

Provision a new AWS Direct Connect connection for each AWS account and connect it back to your on-premises data center.  
Rationale: Provisioning separate Direct Connect connections for each account greatly increases costs and complexity. This strategy defeats the purpose of centralized, scalable connectivity and is not recommended as AWS environments expand.  

Selected  
Provision an AWS VPN CloudHub and connect the AWS accounts directly back to the Direct Connect connection via a VPN connection.  
Rationale: AWS VPN CloudHub is primarily intended for inter-branch connectivity using VPN tunnels over the internet. It does not offer the dedicated link or bandwidth savings of Direct Connect, and it is not designed for integrating on-premises with multiple VPCs via Direct Connect.  



### Question 33
Your organization is launching a globally accessible web application expected to face unpredictable traffic spikes. Leadership requires a scalable AWS architecture that can automatically adjust to demand while keeping compute and network costs low. The design must ensure secure access, high availability, and optimized global performance. Which combination of actions supports these requirements?  

#### Correct Answers
Selected  
Deploy Amazon Elastic Compute Cloud (Amazon EC2) Auto Scaling groups behind an Application Load Balancer to automatically scale compute resources based on demand.  
Rationale: EC2 Auto Scaling combined with an Application Load Balancer adds or removes instances automatically, ensuring compute cost matches actual usage and preventing overprovisioning for unpredictable workloads.  

Distribute edge content using Amazon CloudFront and configure the web application to serve static assets from Amazon Simple Storage Service (S3).  
Rationale: Using CloudFront caches content close to users globally, reducing data transfer costs and latency. Serving static files from S3 is more economical than hosting all assets on compute resources.  

Selected  
Use AWS Global Accelerator to provide a single-entry point and latency-based routing that can optimize network paths for global users.  
Rationale: AWS Global Accelerator improves global app performance by routing users to the optimal AWS endpoint, reducing network hops and optimizing data transfer cost efficiency for distributed workloads.  

#### Incorrect Answers  
Place all compute resources in a single Availability Zone to reduce inter-AZ network costs regardless of the workload's scale.  
Rationale: Reducing to a single Availability Zone lowers some costs but introduces single points of failure. High availability and resilience demand a multi-AZ design, which is essential for most production workloads.  

Provision On-Demand Amazon EC2 instances sized for maximum peak traffic and configure the app for manual scaling only during traffic spikes.  
Rationale: Sizing resources to peak demand always incurs higher costs due to underutilization during normal periods. Manual scaling increases operational overhead and does not take advantage of AWS cost-saving elasticity.  

Use Network Load Balancer and only IPv6 addressing to eliminate all public internet gateways and stop using content delivery services.  
Rationale: Removing public gateways and CDNs like CloudFront can reduce security but increases latency and potentially raises costs from less efficient network routing and direct transfers for global users.  









