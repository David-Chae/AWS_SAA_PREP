Design High-Performing Architectures
10 of 13 correct


Question 1
You manage a serverless e-commerce platform that logs user activity. During sales events, traffic spikes lead to Amazon RDS connection pool exhaustion and timeouts. How can you prevent excessive open connections and reduce service disruptions during peak loads?

Correct Answers
Implement Amazon Relational Database Service (RDS) Proxy.

Rationale: Amazon Relational Database Service (RDS) Proxy helps manage and multiplex database connections, preventing pool exhaustion by reusing existing connections. It efficiently handles connection surges from serverless workloads, reduces timeouts, and improves application reliability during traffic spikes.

Incorrect Answers
Configure Amazon Route 53 Health Checks.

Rationale: Route 53 Health Checks monitor endpoint health and update DNS records accordingly but do not help manage or limit concurrent database connections. They do not help with pool exhaustion or minimize disruptions due to excess connections in this scenario.

Selected
Utilize AWS Auto Scaling for Amazon Relational Database Service (RDS).

Rationale: AWS Auto Scaling can scale read replicas or instance size for Amazon Relational Database Service (RDS) based on metrics, but it does not multiplex client connections or address connection pool exhaustion caused by bursty, serverless behavior.

Optimize database indexing.

Rationale: Optimizing database indexing improves query performance but does not manage the number of concurrent client connections or prevent connection pool exhaustion. Indexes help with speed, not with connection limits during high-load situations.



Question 4
You are designing the compute layer for a real-time analytics platform that receives highly variable traffic during marketing campaigns. The platform must scale automatically based on demand while minimizing instance startup time. It must remain highly available during scaling events and infrastructure failure. What actions should you take to meet these requirements?

Correct Answers
Selected
Use an Amazon EC2 Auto Scaling group with mixed instances across multiple Availability Zones.

Rationale: Mixed instances improve availability and cost-efficiency; multiple Availability Zones ensure high availability.

Selected
Enable instance warm pools for the Amazon EC2 Auto Scaling group.

Rationale: Warm pools reduce instance startup time, allowing faster response to traffic spikes.

Incorrect Answers
Use only On-Demand Instances in a single Availability Zone.

Rationale: Using one zone limits availability; On-Demand alone increases cost and lacks resiliency.

Use EC2 Spot Instances exclusively to serve all traffic.

Rationale: Spot Instances can be interrupted and do not guarantee availability, making them unsuitable as the sole compute layer.

Provision an Amazon EC2 Auto Scaling group with scheduled scaling.

Rationale: Scheduled scaling does not adapt to unexpected or real-time changes in traffic demand.



Question 6
You are the database architect for a biotechnology company developing a genomics data platform. The platform requires a database solution that supports complex, ad hoc analytical queries on large, semi-structured datasets while maintaining durability and scalability. It must integrate easily with machine learning workflows and must support ACID semantics for transactional metadata operations. Which AWS database service should you design to meet these requirements?

Correct Answers
Selected
Use Amazon DocumentDB (with MongoDB compatibility) to store and query semi-structured genomics data.

Rationale: Amazon DocumentDB enables scalable, fully managed document database capabilities ideal for large semi-structured datasets, supports ACID transactions for metadata operations, and integrates well with analytics and machine learning pipelines.

Incorrect Answers
Use Amazon Redshift as the primary database for all genomics data storage and transactional operations.

Rationale: Amazon Redshift is optimized for structured data warehousing and analytics but does not support ACID transactions required for metadata or transactional operations in the genomics application.

Use Amazon Keyspaces (for Apache Cassandra) to handle the semi-structured data.

Rationale: Amazon Keyspaces offers scalability for key-value workloads but lacks strict ACID compliance necessary for transactional metadata operations and complex ad hoc queries required by the genomics platform.

Use Amazon Neptune to store the genomics data.

Rationale: Amazon Neptune is optimized for highly connected graph data but is not designed for large volumes of semi-structured data or integration with general analytics and ML workflows common in genomics platforms.



Question 10
You are designing a compute infrastructure for a social media analytics platform that experiences highly variable traffic patterns throughout the day. The solution must automatically scale compute resources in response to load changes, maintain high availability, and reduce the operational burden of infrastructure management. Which actions should you take to meet these requirements?

Correct Answers
Selected
Configure Amazon ECS with AWS Fargate to run containers.

Rationale: AWS Fargate provides serverless container execution with automatic scaling and reduces management overhead.

Selected
Enable Application Auto Scaling on Amazon ECS services.

Rationale: Application Auto Scaling dynamically adjusts tasks based on demand, providing elasticity for container workloads.

Incorrect Answers
Deploy Amazon ECS services on Amazon EC2 instances using scheduled scaling policies.

Rationale: Scheduled scaling does not respond instantly to unpredictable workload changes, limiting elasticity.

Use Amazon EC2 instances with Elastic Load Balancing to distribute traffic.

Rationale: Elastic Load Balancing distributes traffic but does not directly control automatic scaling of compute resources.

Deploy containers on Amazon Lightsail with load balancer enabled.

Rationale: Lightsail provides basic container hosting but lacks advanced elastic scaling features required for this workload.




Question 12
You are designing a new global user analytics system for a mobile gaming company. The database layer must support write-heavy workloads from millions of devices worldwide. It must also deliver low-latency read access for frequently queried user session data. The read traffic will be highly variable and peak during global events. What should you implement?

Correct Answers
Selected
Use Amazon DynamoDB with on-demand capacity mode and enable DynamoDB Accelerator (DAX) for read performance.

Rationale: DynamoDB handles unpredictable write traffic with on-demand mode, and DAX significantly improves read latency at scale.

Incorrect Answers
Use Amazon RDS for MySQL with Multi-AZ deployments and provisioned IOPS storage.

Rationale: RDS for MySQL can become a bottleneck under massive write throughput and does not scale as efficiently for global workloads.

Use Amazon Redshift with concurrency scaling enabled.

Rationale: Redshift is optimized for analytical queries, not high-throughput transactional writes from millions of devices.

Use Amazon Aurora Serverless v2 with read replicas in a single Region.

Rationale: Aurora Serverless v2 scales well, but cross-Region latency and write-heavy demands reduce performance and global coverage.



Question 19
A healthcare startup needs to collect real-time telemetry data from thousands of connected medical devices. The data must be ingested and validated, and the format normalized before storing the clean records in Amazon Simple Storage Service (Amazon S3). The solution must handle variable load patterns, including traffic bursts, and minimize operational overhead. What actions should you take to meet these requirements?

Correct Answers
Selected
Use AWS IoT Core to ingest and route the device data through an AWS Lambda function for validation and normalization.

Rationale: AWS IoT Core can securely ingest real-time device data, and AWS Lambda enables lightweight transformation without managing servers.

Selected
Use AWS Lambda to process the data and store the validated results directly in Amazon S3.

Rationale: AWS Lambda allows scalable, event-driven processing and direct integration with Amazon S3 for clean, structured data storage.

Incorrect Answers
Use AWS Step Functions to create a workflow that periodically pulls device data and stores it in Amazon S3.

Rationale: AWS Step Functions is not designed for real-time ingestion and cannot directly ingest streaming data from devices.

Use Amazon Redshift to ingest and transform the raw telemetry data from the devices in real time.

Rationale: Amazon Redshift is a data warehouse service and is not intended for direct ingestion of high-velocity streaming telemetry data.

Use Amazon Aurora to store the raw data and periodically trigger ETL jobs using AWS Glue to move the data to Amazon S3.

Rationale: This introduces unnecessary complexity and does not meet the real-time ingestion or transformation requirement of the scenario.



Question 26
You work for a travel reservation company that manages hotel and flight bookings globally. The company needs to migrate its on-premises relational booking database to AWS. The workload experiences predictable read/write operations with occasional spikes during holidays and sales. Management requires a highly available solution with minimal administrative overhead and optimized performance. What is the most suitable Amazon database service for this scenario?

Correct Answers
Selected
Use Amazon Aurora with Aurora Replicas in multiple Availability Zones.

Rationale: Provides high availability, automated scaling, and performance optimization with minimal administration.

Incorrect Answers
Use Amazon RDS on a single Availability Zone with provisioned instances.

Rationale: Does not provide high availability; a single Availability Zone setup is a single point of failure.

Use Amazon RDS with Multi-AZ deployments and manual backups.

Rationale: Although highly available, manual backups introduce unnecessary administration and do not improve performance.

Use Amazon DynamoDB with on-demand capacity mode.

Rationale: DynamoDB is not a relational database and would require application refactoring to support its data model.



Question 27
A team is building a real-time content analysis system that processes large volumes of event-based data. The data is stored temporarily for batch processing and automatically deleted after processing. The solution must support high-throughput parallel access and scale without requiring server management. Which storage solution should the team use?

Correct Answers
Use Amazon S3 with lifecycle policies and S3 Transfer Acceleration enabled.

Rationale: Amazon S3 supports parallel access, lifecycle-based deletion, and auto-scaling with high-throughput capabilities.

Incorrect Answers
Selected
Use Amazon EBS volumes attached to compute-optimized Amazon EC2 instances.

Rationale: Amazon EBS requires instance management and is not ideal for highly parallel, short-lived storage requirements.

Use Amazon FSx for Lustre configured as a standalone file system.

Rationale: FSx for Lustre as a standalone system lacks elastic scalability and cost-efficiency for transient data workloads.

Use Amazon EFS with a lifecycle management policy and throughput mode set to bursting.

Rationale: Amazon EFS is not optimized for object-based storage and introduces unnecessary overhead for temporary data.




Question 31
You are designing a compute solution for a startup that runs containerized web applications. Traffic fluctuates unpredictably throughout the day, sometimes with sudden spikes. The company requires a fully managed, elastic compute service that removes the need to provision or manage servers, and that scales automatically based on incoming requests. What should you recommend?

Correct Answers
Selected
Use AWS Fargate to run containers with Amazon Elastic Container Service (Amazon ECS).

Rationale: AWS Fargate runs containers serverless, automatically scaling based on workload without managing infrastructure.

Incorrect Answers
Use Amazon EC2 instances with Auto Scaling groups to host containers manually.

Rationale: This requires managing servers and does not eliminate operational overhead.

Use Amazon Elastic Kubernetes Service (Amazon EKS) on Amazon EC2 with fixed node counts.

Rationale: Fixed node counts limit elasticity and requires infrastructure management.

Deploy containers on Amazon Lightsail instances with scheduled scaling.

Rationale: Lightsail does not support serverless scaling and requires manual resource management.



Question 38
You are the administrator of a media company’s website that hosts large static assets in an Amazon Simple Storage Service (Amazon S3) bucket. Users globally experience slow download speeds and intermittent failures when accessing the assets. After verifying stable network connectivity, what actions improve both availability and performance of the assets?

Correct Answers
Selected
Enable Amazon CloudFront as a content delivery network in front of the Amazon S3 bucket.

Rationale: CloudFront caches content at edge locations, reducing latency and improving availability by offloading the origin.

Selected
Enable Amazon S3 Cross-Region Replication to replicate data to another AWS Region.

Rationale: Cross-Region Replication improves data availability and resilience by replicating data across regions.

Incorrect Answers
Increase the number of Amazon S3 buckets to distribute load.

Rationale: Amazon S3 automatically scales; bucket count does not affect availability or performance.

Migrate the static assets from Amazon S3 to Amazon Elastic File System (Amazon EFS).

Rationale: Amazon EFS is designed for shared file storage, not optimized for high-availability global static asset hosting.

Disable versioning on the Amazon S3 bucket to reduce overhead during retrieval.

Rationale: Versioning does not affect read performance or availability; disabling it reduces data protection.

Disable server-side encryption on Amazon S3 buckets to increase upload speed.

Rationale: Disabling encryption compromises security and generally has negligible impact on upload performance.



Question 47
You are the lead data engineer for a large streaming media company that needs to build a scalable data ingestion architecture for daily log and event data generated by millions of devices worldwide. The solution must ingest flat files continuously uploaded to Amazon S3, transform and normalize data in near real time, and catalog results for immediate analytics queries with minimal operational overhead and fully managed scaling. Which AWS architecture best addresses these requirements?

Correct Answers
Selected
Use AWS Glue to create serverless ETL jobs that continuously process new S3 data, perform transformation and normalization, and catalog outputs for analytics.

Rationale: AWS Glue is designed for continuous, event-driven or scheduled data ingestion from S3, near real-time transformation using serverless ETL jobs, and integration with the AWS Glue Data Catalog for immediate analytics with minimal management.

Incorrect Answers
Use AWS DataSync to move data from Amazon S3 to Amazon Redshift and run scheduled batch SQL scripts to process and transform data.

AWS DataSync is optimized for large-scale data migrations, not continuous, automated processing. Batch SQL scripts in Amazon Redshift are higher latency and require managing warehouse resources for transformation.

Use AWS Transfer Family to ingest log files into Amazon S3, transform data using Amazon EC2-based ETL applications, and store results in Amazon DynamoDB.

Rationale: AWS Transfer Family is for file transfers using SFTP and similar protocols; EC2-based ETL adds significant management overhead, and DynamoDB is not optimized for large-scale, transformed log analytics data.

Use an AWS Snowball Edge appliance to upload new files to Amazon S3 on a daily basis, transform data in Amazon Elastic MapReduce (Amazon EMR), and catalog results with Amazon SimpleDB.

Rationale: AWS Snowball Edge is for offline or hybrid bulk data transfer, not continuous cloud-based ingestion. Amazon EMR is designed for large-scale batch processing, and Amazon SimpleDB is outdated and does not support modern analytics workloads.



Question 49
You are the lead network specialist for a global insurance provider tasked with connecting multiple AWS Virtual Private Clouds (VPCs) in different regions for claims processing across business units. The solution must enable private API sharing between units, restrict service access by department, avoid public internet exposure, and allow efficient onboarding of new VPCs with minimal manual configuration and low operational overhead. Which AWS services and features should you include?

Correct Answers
Selected
Use AWS PrivateLink to publish and consume APIs privately between VPCs, isolating service endpoints from the public internet.

Rationale: AWS PrivateLink enables secure, private connectivity for internal services between VPCs and accounts, reducing attack surface and simplifying network management.

Selected
Use AWS Resource Access Manager (AWS RAM) to share VPC subnets and PrivateLink endpoints for quick onboarding of new business units.

Rationale: AWS Resource Access Manager allows centralized sharing of subnets and endpoints, minimizing manual network configuration and supporting efficient onboarding of additional VPCs.

Incorrect Answers
Set up public-facing Application Load Balancers with IAM authentication for all internal APIs.

Rationale: Public-facing load balancers expose services to the internet, violating the isolation requirement and increasing security risks even if access is authenticated.

Build a custom site-to-site VPN mesh between each VPC, with manual route and firewall updates for each connection.

Rationale: VPN meshes create complex, hard-to-manage networks, require manual configuration for each new VPC, and are inefficient for scalable private VPC communication.

Use Amazon CloudFront distributions with signed URLs to provide private access to APIs across business units.

Rationale: Amazon CloudFront is designed for content delivery, not private intra-VPC API sharing. It cannot natively restrict access to internal services not exposed to the internet.



Question 52
You are designing a web application architecture that uses load balancers to distribute traffic to an Auto Scaling Group of Amazon Elastic Compute Cloud (EC2) instances spanning multiple Availability Zones. You are choosing between an Application Load Balancer and a Classic Load Balancer. Which feature is only supported by the Application Load Balancer?

Correct Answers
Path-based routing for HTTP and HTTPS requests

Rationale: Application Load Balancer supports advanced Layer 7 routing features such as path-based routing, enabling traffic to be routed based on URL paths. Classic Load Balancer does not support path-based routing and only routes at Layer 4.

Incorrect Answers
Support for Amazon EC2-Classic networking

Rationale: Classic Load Balancer supports EC2-Classic environments, which are legacy networks. Application Load Balancer works only within Virtual Private Cloud (VPC) and does not support EC2-Classic.

TCP and SSL listeners for Layer 4 traffic.

Rationale: Classic Load Balancer supports TCP and SSL listeners allowing Layer 4 load balancing. Application Load Balancer supports only HTTP and HTTPS (Layer 7). TCP/SSL requires Classic or Network Load Balancer in AWS.

Selected
Custom SSL security policies configuration.

Rationale: Classic Load Balancer allows custom SSL security policies with specific cipher suites. Application Load Balancer uses predefined security policies and does not allow customization of SSL policies.
