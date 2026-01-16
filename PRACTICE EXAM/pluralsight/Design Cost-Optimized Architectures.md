Design Cost-Optimized Architectures
11 of 12 correct

Question 8
A streaming analytics company migrated its production workloads to AWS. Last month, the company experienced unexpected spikes in network costs. Analysis shows:

High internet traffic accessing static assets stored in Amazon S3.
Cross-AZ traffic due to microservice communication and NAT Gateway usage.
Cross-account microservices accessing S3 over public endpoints.
What actions should you take to optimize network architecture and reduce cost?

Correct Answers
Selected
Configure Amazon S3 VPC endpoints in each VPC to allow private access to S3 from applications and microservices.

Rationale: Using VPC endpoints enables private, in-cloud access to S3 traffic, eliminating unnecessary routing over the internet and reducing NAT Gateway and cross-AZ transfer charges for S3 data access.

Deploy internal Application Load Balancers (ALB) for microservice-to-microservice communication within the same Availability Zone.

Rationale: Internal ALBs keep east-west traffic within a single AZ, lowering cross-AZ charges and optimizing internal network routing.

Review NAT Gateway placement and scale horizontally by deploying one NAT Gateway per Availability Zone to minimize cross-AZ data transfer fees.

Rationale: NAT Gateway cost increases when resources in one AZ cross to another for outbound traffic. Placing a NAT Gateway in each AZ keeps traffic local and reduces per-GB cross-AZ costs.

Incorrect Answers
Route all S3 access through a central NAT Gateway in the primary Availability Zone to simplify monitoring.

Rationale: Centralizing NAT Gateway forces cross-AZ traffic for other AZs, significantly increasing inter-AZ transfer charges and failing to address internet egress cost for S3 traffic.

Replace Application Load Balancers with Network Load Balancers for all internal services to reduce cost.

Rationale: Network Load Balancers are intended for high-throughput, TCP/UDP services and are rarely more cost-effective for HTTP/HTTPS microservices. They do not optimize internal communication pathing or S3 access cost.



Question 11
You are a cloud architect at an insurance company who, for compliance reasons, must store customer data for ten years before deleting it. The company needs to keep storage costs as low as possible, and retrieval times of up to 24 hours are acceptable. Which Amazon Simple Storage Service (S3) storage class should you recommend minimizing costs?

Correct Answers
Selected
Amazon S3 Glacier Deep Archive

Rationale: Amazon S3 Glacier Deep Archive is the lowest-cost storage class for long-term archival. It is designed to retain data for years and supports retrieval times within 24 hours, making it ideal for compliance data that is rarely accessed but must be preserved cost-effectively.

Incorrect Answers
Amazon S3 Intelligent-Tiering

Rationale: Amazon S3 Intelligent-Tiering optimizes costs for unpredictable access patterns but is not as inexpensive as other data services requiring long-term, rarely accessed storage.

Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA)

Rationale: Amazon S3 One Zone-IA offers low-cost storage with rapid access, but it stores data in a single Availability Zone and costs more than other data storage alternative for deep, long-term archives.

Amazon S3 Standard

Rationale: Amazon S3 Standard provides the highest durability and availability with instant access, but it is geared toward frequently accessed data and carries the highest storage cost among these classes.
Consolidate all public APIs and dashboards on instances in a single AZ to save on multi-AZ data transfer.

Rationale: Hosting all public endpoints in a single AZ sacrifices fault tolerance and high-availability best practices and does not address the root causes of the network cost spikes.


Question 17
A marine research organization is deploying thousands of sensor buoys across global ocean regions. Each buoy collects telemetry and weather data, uploading it to AWS via intermittent satellite internet. The buoys are power-constrained and must minimize data transfer and infrastructure costs. What design actions best support secure, low-cost data ingestion and central storage in AWS?

Correct Answers
Selected
Use Amazon Web Services Internet of Things (AWS IoT) Core to securely ingest buoy data using message queuing telemetry transport (MQTT), over existing satellite links.

Rationale: AWS IoT Core supports lightweight MQTT messaging, ideal for low-bandwidth, intermittent devices. It enables secure, efficient connectivity without needing persistent links or high throughput.

Selected
Route incoming buoy data through AWS IoT rules to store messages in Amazon Simple Storage Service (Amazon S3) for durable, low-cost storage.

Rationale: Using AWS IoT rules to route sensor data to Amazon S3 allows scalable ingestion while minimizing storage costs. S3 is highly durable, pay-as-you-go, and ideal for time-series and batch analytics.

Incorrect Answers
Deploy Site-to-Site VPN tunnels from each buoy to a Virtual Private Cloud (VPC) in AWS to encrypt incoming connections.

Rationale: Site-to-Site VPN requires persistent IP connectivity, expensive satellite bandwidth, and significant administrative effort, making it too costly and heavy for large fleets of remote sensors.

Backhaul buoy traffic to an on-premises data center and forward data from there to AWS over AWS Direct Connect.

Rationale: Routing traffic through an on-premises data center over Direct Connect is costly, introduces latency, and contradicts the need to minimize infrastructure and transfer charges from remote devices.

Place a Network Load Balancer in each Region to directly handle device telemetry over TCP and route traffic to upstream ingestion services.

Rationale: Network Load Balancers are not suitable for constrained devices using message queuing telemetry transport (MQTT) or intermittent connections. They also incur higher per-hour and per-request costs, which are unnecessary for this workload.



Question 24
You are implementing a regional logistics tracking platform that records near real-time events such as fleet location updates, delivery confirmations, and sensor alerts. Event data must be processed immediately, queried by regional offices with low latency, and retained for compliance for at least one year. The solution must minimize database costs while meeting performance, durability, and retention requirements across all regions. Which actions should you take to implement the solution?

Correct Answers
Selected
Use Amazon DynamoDB global tables for event ingestion and real-time reads from regional offices.

Rationale: Amazon DynamoDB global tables allow low-latency, multi-region reads and writes. This avoids cross-region transfer costs and supports instant access for local offices using a fully managed and scalable database service.

Selected
Configure Amazon DynamoDB Time to Live (TTL) to automatically expire items after 30 days, enable DynamoDB Streams to capture removed items, and export expired records to Amazon Simple Storage Service (S3).

Rationale: By activating TTL and streams, expired events are deleted from the active table and captured in DynamoDB Streams. A Lambda function archives the deleted records to Amazon S3, removing old data to reduce database cost while preserving compliance retention outside DynamoDB.

Selected
Apply Amazon S3 Lifecycle policies to transition historical objects to Amazon S3 Glacier Flexible Retrieval after 90 days.

Rationale: Lifecycle policies reduce storage cost by moving older data to archival classes. This ensures long-term retention while minimizing cost for infrequently accessed data older than 90 days.

Incorrect Answers
Use Amazon Neptune in each region to store graph-based fleet relationships, and configure cross-region exports to Amazon S3.

Rationale: Amazon Neptune is a graph database not intended for time-series or event tracking at scale. It increases complexity and does not support automatic TTL or managed multi-region infrastructure for this use case.

Create a Multi-AZ Amazon Relational Database Service (Amazon RDS) instance with continuous backups to Amazon S3.

Rationale: Amazon RDS offers reliable relational data services but is not cost-optimized for high-volume, high-velocity event streams. Multi-AZ configurations increase cost and lack native TTL and global low-latency capabilities.

Store all ingestion and reporting data in a centralized Amazon Aurora cluster and use Amazon CloudFront for read optimization.

Rationale: Amazon Aurora is a high-performance relational database but is not ideal for globally distributed write-heavy workloads or scalable time-limited TTL storage. CloudFront does not cache dynamic query results from databases.



Question 28
You work for an advertising company that delivers high-resolution images and videos to users worldwide. As part of your AWS migration, you must design a solution that delivers large media files at high speed while minimizing delivery and infrastructure costs. Which approach best meets these requirements?

Correct Answers
Selected
Use Amazon Simple Storage Service (S3) with Amazon CloudFront to deliver media files globally.

Rationale: Amazon S3 offers durable storage, while CloudFront is AWS’s global content delivery network (CDN) that caches and serves files rapidly to users worldwide, reducing latency and offloading S3 bandwidth for cost efficiency.

Incorrect Answers
Build your own CDN network with hundreds of servers across the globe and use Amazon Route 53 for geo-routing.

Rationale: Building and maintaining a custom CDN is highly expensive and complex, requiring management of global infrastructure, software, and traffic engineering. Amazon Route 53 provides DNS-based routing, not cache distribution.

Upload files to Amazon Elastic File System (EFS) and use Amazon Elastic Compute Cloud (EC2) to serve content globally.

Rationale: Serving content from EFS via EC2 instances does not deliver the scalability or cost advantages of a managed CDN. This approach increases operational overhead and bandwidth costs and is not designed for massive global content delivery.

Use Amazon DynamoDB Accelerator (DAX) as a CDN to serve content globally.

Rationale: DynamoDB Accelerator (DAX) is a caching layer for accelerating access to DynamoDB items; It is not a CDN and cannot be used to serve static media files to global users. It is not intended for large file/media distribution.



Question 33
A market research company uses a relational database hosted on Amazon Relational Database Service (Amazon RDS) for its primary reporting platform. Finance reviews have identified a persistent, unexpected rise in monthly database costs. On investigation, you observe the following:

The Amazon RDS database is provisioned with high-capacity storage volumes and performance settings well above current workloads.
Multiple unused database snapshots and old automated backups remain in place, incurring additional storage charges.
Reporting and analytics queries are performed directly on the production instance during business hours.
No lifecycle or automated archival processes are in place for large, infrequently accessed tables.
The database is deployed with Multi-AZ for failover, but business requirements can tolerate multi-hour downtime in case of a failure.
What actions should you take to reduce ongoing database costs while ensuring data remains available and protected to meet current requirements?

Correct Answers
Selected
Delete unused Amazon RDS snapshots and remove previous automated backups that exceed retention policies.

Rationale: Retaining unnecessary database snapshots and outdated automated backups increases storage costs. Removing obsolete or redundant backups reduces expenses without impacting current data availability or protection requirements.

Selected
Review provisioned storage and adjust Amazon RDS volume types and performance settings to fit actual usage patterns.

Rationale: Oversized storage volumes and excessive performance parameters lead to higher ongoing charges. Regularly resizing volumes and adjusting parameters to match workload needs delivers immediate and ongoing cost savings.

Selected
Move infrequently accessed historical tables to separate low-cost storage, such as Amazon Simple Storage Service (S3), and implement lifecycle archival policies.

Rationale: Large tables that are rarely queried do not need to stay in active database storage. Offloading them to Amazon S3 and applying lifecycle rules lowers database size and cost while preserving access and compliance with company data policies.

Incorrect Answers
Disable Multi-AZ deployments and remove automated backups for the production database to reduce costs.

Rationale: Removing all redundancy and backup protection may eliminate some costs but exposes the database to significant risk of prolonged outages and data loss, violating basic operational protection and recovery requirements.

Schedule full database exports to Amazon Redshift and shut down the Amazon RDS instance each night to save on database runtime charges.

Rationale: Exporting data to Amazon Redshift adds costs for a separate analytics platform. Shutting down Amazon RDS at night is not supported for all engine types and may block access for processes that run after hours or for global users.




Question 36
A software company is seeking compute capacity in the AWS Cloud to support a fault-tolerant and flexible application. The application is not mission-critical and can tolerate occasional downtime. The company wants to obtain this compute capacity at the lowest possible cost. Which type of Amazon Elastic Compute Cloud (Amazon EC2) servers should it use to meet these requirements?

Correct Answers
Selected
Use Amazon EC2 Spot Instances to run the application.

Rationale: Amazon EC2 Spot Instances let you use spare cloud capacity at discounts of up to 90% over On-Demand prices. They are ideal for fault-tolerant, non-essential workloads that can tolerate interruptions, making them the lowest-cost choice for this use case.

Incorrect Answers
Use Amazon EC2 Reserved Instances to run the application.

Rationale: Amazon EC2 Reserved Instances require a one- or three-year commitment in exchange for partial discounts but do not offer the flexibility or lowest absolute cost for workloads that can tolerate interruptions or downtime.

Use Amazon EC2 On-Demand Instances to run the application.

Rationale: Amazon EC2 On-Demand Instances do not require long-term commitments and provide flexibility but generally cost more than other purchasing options for workloads that can tolerate interruptions.

Use Amazon EC2 Dedicated Hosts to run the application.

Rationale: Amazon EC2 Dedicated Hosts allocate entire physical servers to a client, incurring the highest costs and generally being reserved for requirements around licensing, compliance, or dedicated hardware, not cost-optimized for non-critical or interruptible workloads.




Question 40
You are designing a data architecture for a climate research institute. Researchers frequently update small metadata records used for real-time analysis and occasionally upload large satellite images needed for annual modeling. Metadata must support immediate queries, while image files should be archived with low cost and accessed on demand. Which actions support this design while optimizing for performance and cost?

Correct Answers
Selected
Store metadata in Amazon Aurora Serverless v2 for fast, on-demand queries with automated capacity scaling.

Rationale: Amazon Aurora Serverless v2 can immediately adapt capacity to variable small query workloads, paying only for what is used. This is cost-efficient for unpredictable, bursty metadata queries.

Selected
Store large satellite image files in Amazon Simple Storage Service (S3) using the S3 Intelligent-Tiering storage class to optimize costs automatically.

Rationale: S3 Intelligent-Tiering automatically moves data between frequent and infrequent access tiers without operational overhead, delivering cost savings for sporadic, large file retrieval patterns.

Selected
Use Amazon Athena to query archived satellite imagery metadata stored as Parquet files in Amazon S3 for annual reporting without provisioning database servers.

Rationale: Amazon Athena provides serverless, on-demand interactive querying on data stored in S3 without infrastructure cost, perfect for infrequently run aggregate analyses on archived data.

Incorrect Answers
Use Amazon Relational Database Service (Amazon RDS) provisioned instances to store all metadata and satellite files with routine backups to Amazon Glacier.

Rationale: Provisioned Amazon RDS instances for large file storage incur high continuous costs and backup to Glacier adds complexity; this approach does not optimize cost for rarely accessed large binary data.

Use Amazon DynamoDB for metadata and store satellite images on Amazon Elastic File System (Amazon EFS), accessed directly by researchers.

Rationale: Amazon EFS is more expensive than S3 for large object storage and does not provide tiered cost optimization; DynamoDB is suitable for metadata but coupling with EFS for files results in inefficient cost architecture.

Store both metadata and satellite images in Amazon Redshift and optimize server nodes to minimize cost.

Rationale: Amazon Redshift is designed for structured analytics with frequent queries, not for large file storage or sporadic archival, resulting in inefficient cost and storage usage.




Question 43
You are an architect at an insurance company designing a new application. The application will use a relational database on the backend that must automatically start up, shut down, and scale capacity up or down as needed. The company requires the database to be as cost-effective as possible. Which AWS database service should you choose?

Correct Answers
Selected
Amazon Aurora Serverless.

Rationale: Amazon Aurora Serverless automatically starts up, shuts down, and scales capacity in response to application traffic. Billing is per actual usage, making it highly cost-effective for variable workloads and removing the need for manual scaling.

Incorrect Answers
Amazon Relational Database Service (Amazon RDS).

Rationale: Amazon RDS provides managed relational databases but typically requires you to provision, resize, and manage instance capacity manually. This leads to higher cost or overprovisioning for unpredictable workloads.

Amazon DynamoDB.

Rationale: Amazon DynamoDB is a serverless, fully managed NoSQL database, not a relational database. It is optimized for key-value or document store use cases and not suited for applications that require relational schema and SQL support.

Amazon Neptune.

Rationale: Amazon Neptune is a managed graph database service, designed for graph workloads (such as relationships, social networks). It does not provide the relational model required by the application described in the scenario.



Question 48
You are a cloud architect for a biotechnology research startup. The company is launching a genomic analysis platform that processes large compute jobs submitted intermittently by scientists across different regions. Each job can require dozens of cores for several hours, followed by periods with no activity. The company needs a solution that minimizes ongoing compute costs while ensuring short jobs can start processing without delay and that there is no long-term infrastructure commitment. Which approach best achieves a cost-optimized compute solution for this scenario?

Correct Answers
Selected
Configure AWS Batch to submit jobs that run on Spot capacity in Amazon Elastic Compute Cloud (Amazon EC2), allowing workloads to scale up and down automatically based on pending jobs.

Rationale: AWS Batch launches compute resources only as jobs are submitted, automatically scaling clusters using discounted Spot Instances. This approach prevents idle compute cost, requires no commitment, and supports bursty, large-scale jobs.

Incorrect Answers
Launch Amazon Elastic Compute Cloud (Amazon EC2) Reserved Instances to maintain a ready fleet that can instantly run analysis jobs at any time.

Rationale: Reserved Instances require a one- or three-year commitment and charge for capacity regardless of utilization, making them cost-inefficient for workloads with intermittent and unpredictable submission patterns.

Set up an Amazon Elastic Compute Cloud (Amazon EC2) Auto Scaling group with large On-Demand Instances running continuously to ensure immediate results.

Rationale: Continuously running On-Demand Instances maximizes availability but results in high, ongoing cost unrelated to workload submission, wasting resources during inactive periods.

Deploy Amazon Elastic Container Service (Amazon ECS) with AWS Fargate to continuously run containers that poll for analysis jobs and shut down manually after completion.

Rationale: Manually managing polling containers increases operational overhead and incurs unnecessary cost when idle containers run. AWS Fargate charges for active runtime, and the solution does not scale down automatically with job inactivity.




Question 50
After an IT Steering Committee meeting, you have been assigned to configure a hybrid environment for your company’s compute resources. You are evaluating different connectivity options based on the key requirements: optimizing overall costs and using existing internet connections. Which AWS technology should you implement to best meet these needs?

Correct Answers
Selected
Use AWS Site-to-Site VPN to connect the on-premises network to an Amazon Virtual Private Cloud (VPC) over existing internet connections.

Rationale: AWS Site-to-Site VPN establishes secure hybrid connectivity over the public internet. It utilizes existing company internet connections and provides the lowest up-front and operational costs.

Incorrect Answers
Use VPC Peering to connect your on-premises environment to your Amazon VPC.

Rationale: VPC Peering connects only two Amazon VPCs and does not support direct on-premises to VPC connectivity. It cannot use the public internet for hybrid integration.

Use AWS Direct Connect Gateway to establish connectivity between your on-premises resources and your Amazon VPC over a dedicated line.

Rationale: AWS Direct Connect Gateway requires a dedicated, private physical link, incurring significant setup and recurring charges. It does not utilize the company’s existing internet connection.

Use AWS Direct Connect to create a dedicated high-bandwidth link between your data center and AWS.

Rationale: AWS Direct Connect offers high performance but involves new physical infrastructure and contract costs, rather than using existing internet, making it less cost-effective for most hybrid scenarios.




Question 55
You are a cloud architect at a fintech company that stores its backups on physical tape at its on-premises data center. Regulatory requirements mandate that the backup data be retained for seven years. The backups are accessed only once per year for audit purposes, and delayed retrieval times are acceptable. The company plans to migrate its backup process to the AWS Cloud to reduce storage and management costs. Which combination of actions provides a compliant and cost-effective solution?

Correct Answers
Selected
Deploy AWS Storage Gateway Tape Gateway to store backups as virtual tapes in Amazon Simple Storage Service (S3).

Rationale: AWS Storage Gateway Tape Gateway integrates with existing tape-based backup software and stores backups as virtual tapes in Amazon Simple Storage Service (S3), enabling tape replacement without changes to backup processes.

Selected
Use Amazon S3 lifecycle policies to transition virtual tapes to Amazon S3 Glacier Deep Archive and enforce a seven-year retention period.

Rationale: Lifecycle policies allow automatic archival of objects from Amazon S3 to Amazon S3 Glacier Deep Archive, meeting long-term retention requirements at the lowest storage cost. Compliance retention periods can be specified to automate deletion after seven years.

Incorrect Answers
Use AWS Snowball Edge to perform monthly transfers of backup data to Amazon Elastic Block Store (Amazon EBS) and attach volumes to Amazon Elastic Compute Cloud (Amazon EC2) instances.

Rationale: AWS Snowball Edge is recommended for offline bulk data transfer, not monthly jobs. Amazon Elastic Block Store (Amazon EBS) volumes incur higher ongoing costs and are not designed for cold storage or long-term compliance backup.

Store backup files in Amazon DynamoDB and apply a time-to-live policy to remove data after seven years.

Rationale: Amazon DynamoDB is a NoSQL database and not suitable for storing unstructured backup files. Time-to-live applies at the item level and does not meet archival or compliance-grade retention requirements for backup storage.

Create an Amazon Elastic Compute Cloud (Amazon EC2) instance to run daily backups and store results in Amazon Simple Storage Service (S3) Standard storage class without lifecycle policies or archival rules.

Rationale: Amazon S3 Standard storage incurs higher costs for data retained over long periods. Without lifecycle policies or archival rules, backup data remains in the default class indefinitely, violating cost optimization and best-practice archiving standards.
