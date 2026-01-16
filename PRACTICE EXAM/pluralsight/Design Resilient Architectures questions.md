Design Resilient Architectures
10 of 17 correct

Question 2
A company has an Auto Scaling group of Amazon Elastic Compute Cloud (EC2) instances hosting its retail sales application. Any significant downtime can result in significant profit loss. The solution architecture also includes an Application Load Balancer and an Amazon Relational Database Service (Amazon RDS) database in a Multi-AZ deployment. What occurs automatically to maintain high availability if the primary database instance fails?

Correct Answers
Selected
The CNAME is switched from the primary database instance to the secondary.

Rationale: When a Multi-AZ Amazon RDS deployment detects a primary instance failure, the system automatically updates the DNS record to point the database endpoint's CNAME to the standby (secondary) instance, minimizing downtime.

Incorrect Answers
The Elastic IP address for the primary database is moved to the secondary database.

Rationale: Amazon RDS does not use Elastic IP addresses for failover or instance endpoint management. RDS endpoints are managed through DNS names, not static IP addresses.

A Lambda function kicks off a CloudFormation template to deploy a backup database.

Rationale: Amazon RDS Multi-AZ failover is automatic; no AWS Lambda or CloudFormation workflow is required to stand up a new instance during a failover event.

Route 53 points the CNAME to the secondary database instance.

Rationale: Amazon RDS automatically manages the DNS name at the AWS RDS service level, not through Amazon Route 53 configuration or manual DNS record updates for endpoints.


Question 5
You work for a major gaming company. The company must distribute gaming traffic using the User Datagram Protocol (UDP) among multiple servers to ensure real-time gameplay and high availability. The application must also store matchmaking and session state data in a NoSQL database for scalability. Which solution supports both requirements?

Correct Answers
Selected
Network Load Balancer and Amazon DynamoDB.

Rationale: A Network Load Balancer supports UDP traffic, making it suitable for gaming workloads that require fast, connectionless communication. Amazon DynamoDB provides a fully managed NoSQL database that is highly scalable and widely used in the gaming industry for session state and matchmaking data.

Incorrect Answers
Application Load Balancer with Amazon Aurora.

Rationale: Application Load Balancers support only HTTP and HTTPS (Layer 7), not UDP, and Amazon Aurora is a relational database, not NoSQL, making this pairing unsuitable for the requirements.

Application Load Balancer with Microsoft SQL Server in RDS.

Rationale: Application Load Balancers do not support UDP, and Microsoft SQL Server in Amazon Relational Database Service (Amazon RDS) is a relational, not a NoSQL, database. This does not fulfill either need.

Network Load Balancer with Amazon Aurora Serverless.

Rationale: While the Network Load Balancer supports UDP, Amazon Aurora Serverless is a relational, not NoSQL, database, and is therefore not optimal for NoSQL gaming workloads.

Give Feedback


Question 5
You work for a major gaming company. The company must distribute gaming traffic using the User Datagram Protocol (UDP) among multiple servers to ensure real-time gameplay and high availability. The application must also store matchmaking and session state data in a NoSQL database for scalability. Which solution supports both requirements?

Correct Answers
Selected
Network Load Balancer and Amazon DynamoDB.

Rationale: A Network Load Balancer supports UDP traffic, making it suitable for gaming workloads that require fast, connectionless communication. Amazon DynamoDB provides a fully managed NoSQL database that is highly scalable and widely used in the gaming industry for session state and matchmaking data.

Incorrect Answers
Application Load Balancer with Amazon Aurora.

Rationale: Application Load Balancers support only HTTP and HTTPS (Layer 7), not UDP, and Amazon Aurora is a relational database, not NoSQL, making this pairing unsuitable for the requirements.

Application Load Balancer with Microsoft SQL Server in RDS.

Rationale: Application Load Balancers do not support UDP, and Microsoft SQL Server in Amazon Relational Database Service (Amazon RDS) is a relational, not a NoSQL, database. This does not fulfill either need.

Network Load Balancer with Amazon Aurora Serverless.

Rationale: While the Network Load Balancer supports UDP, Amazon Aurora Serverless is a relational, not NoSQL, database, and is therefore not optimal for NoSQL gaming workloads.

Give Feedback


Question 18
You lead a small development team at a Limited Liability Company (LLC). Your team is planning the development of a full-stack web application that uses Next.js with server-side rendering (SSR) on the frontend. The team wants to use AWS for hosting and deployment but lacks in-depth experience with AWS infrastructure. To reduce operational complexity, the team prefers a managed service that simplifies both development and deployment of their application. Which AWS service should the team select to meet these requirements?

Correct Answers
AWS Amplify.

Rationale: AWS Amplify is a fully managed service designed to simplify the development, deployment, and hosting of full-stack web applications, including native support for Next.js with server side rendering (SSR). It is optimized for teams that want to avoid complex AWS infrastructure management.

Incorrect Answers
Selected
Amazon Elastic Kubernetes Service (Amazon EKS) with Amazon DynamoDB.

Rationale: Amazon Elastic Kubernetes Service (Amazon EKS) is a powerful managed Kubernetes platform but requires significant container, networking, and operational expertise, making it unsuitable for teams seeking simplicity.

AWS AppSync.

Rationale: AWS AppSync is a managed service for building GraphQL APIs and connecting to data sources, but it does not manage or deploy entire full-stack applications or provide SSR hosting for Next.js out of the box.

AWS Lambda with Amazon Relational Database Service (Amazon RDS).

Rationale: This is a complex architecture, especially with their limited experience. Furthermore, it does not provide any frontend capabilities. There is a simpler, managed solution.


Question 21
You work for a real estate company that has many different batch processes to automate, such as patch management and data synchronization. You need to automate these tasks and integrate the processes with AWS services. You also want the solution to be serverless if possible. Which AWS service should you use?

Correct Answers
Selected
AWS Step-Functions

Rationale: AWS Step Functions is a serverless orchestration service that allows you to coordinate multiple AWS services into automated workflows. It is purpose-built for automating batch and business processes in a serverless manner.

Incorrect Answers
AWS X-Ray

Rationale: AWS X-Ray is a distributed tracing and debugging service for applications. It does not automate processes or provide orchestration of batch operations.

AWS Batch Manager

Rationale: AWS Batch Manager is not an AWS service. The correct managed AWS batch processing solution is AWS Batch, which is not serverless and not named "Batch Manager."

AWS Batch Assist

Rationale: AWS Batch Assist is not a real AWS service. AWS Batch exists as a managed batch computing service, but "Assist" is not a component nor a feature, and AWS Batch is not inherently serverless.



Question 22
You work for an online retailer where any downtime can result in significant loss of revenue. Your application is deployed on an Auto Scaling group of Amazon Elastic Compute Cloud (EC2) instances behind a load balancer. You have used AWS CloudFormation to deploy your resources. The Auto Scaling group is using default settings and a simple CPU utilization scaling policy, spanning multiple Availability Zones for high availability. The load balancer performs health checks using an HTML file generated by a script. During load testing, you observe in Amazon CloudWatch that the load balancer is not sending traffic to one of the Amazon EC2 instances. What could be the cause?

Correct Answers
Selected
The Amazon Elastic Compute Cloud (EC2) instance has failed the load balancer health check.

Rationale: If an Amazon EC2 instance fails the health check configured by the load balancer, it is automatically marked as unhealthy and removed from the target set, so no traffic is routed to that instance.

Incorrect Answers
The instance has not been registered with Amazon CloudWatch.

Rationale: Registration with Amazon CloudWatch is not required for an Amazon EC2 instance to receive traffic from a load balancer. CloudWatch is a monitoring tool, not part of routing or registration logic.

The Amazon Elastic Compute Cloud (EC2) instance has failed Amazon EC2 status checks.

Rationale: Failing Amazon EC2 status checks would cause the instance to be replaced by the Auto Scaling group. Instances failing only EC2 status checks are typically terminated and replaced, not just deregistered from traffic by the load balancer.

You are load testing at a moderate traffic level and not all instances are needed.

Rationale: Even at moderate traffic levels, the load balancer distributes requests among all healthy registered instances. The number of needed instances does not prevent traffic from being routed to any healthy instance.


Question 23
Your company is building out a second AWS Region. To follow best practices, it has used AWS CloudFormation to simplify the migration. However, when running the CloudFormation template in the new region, the template continues to reference the Amazon Machine Image (AMI) from the original region. What is the best solution to have the correct AMI automatically selected whenever the template is deployed in a new region?

Correct Answers
Create a mapping in the template. Define the unique AMI value per region.

Rationale: Using the Mappings section in the template, you can map each AWS Region to its specific AMI ID. When the template is deployed, the correct AMI for the target region is selected automatically using !FindInMap with AWS::Region.

Incorrect Answers
Selected
Create a condition in the template to automatically select the correct AMI ID.

Rationale: Conditions in CloudFormation control resource creation or configuration, not dynamic value lookup by region. They are not used to select region-specific AMIs automatically.

Create a Parameter section in the template. Whenever the template is run, fill in the correct AMI ID.

Rationale: Parameters require manual entry or automated injection at stack launch, increasing the risk of errors and reducing automation. This does not achieve fully automated regional selection.

Update the AMI in the old region, as AMIs are universal.

Rationale: AMIs are region-specific resources. An AMI in one region cannot be referenced in another region using the same ID. AMIs must be copied between regions as needed.


Question 32
A company has an application for sharing static content, such as photos. As usage grows globally, the company faces higher latency for users. What AWS services can host a static website, serve content to worldwide users, and address latency and cost concerns?

Correct Answers
Use Amazon CloudFront to serve content globally by caching images from Amazon Simple Storage Service (Amazon S3) to reduce latency and cost.

Rationale: Amazon CloudFront is a content delivery network that delivers static content from edge locations close to users. It integrates seamlessly with Amazon S3, improving latency and minimizing data transfer costs.

Incorrect Answers
Use AWS Global Accelerator directing traffic to Application Load Balancers in each region, with EC2 instances accessing a shared Amazon Elastic File System volume.

Rationale: AWS Global Accelerator is designed for improving availability and performance of non-HTTP/S applications, but using EC2 and Amazon Elastic File System adds unnecessary complexity and cost for serving static content.

Selected
Host a static website on Amazon Simple Storage Service (Amazon S3) with cross-region replication and use Amazon Route 53 geolocation routing to serve users from the nearest region.

Rationale: S3 static website hosting supports basic static content delivery, but cross-region replication and Amazon Route 53 geolocation routing significantly increase management overhead and costs without delivering CDN-level latency improvements.

Use AWS CloudFormation to deploy static content hosted on Amazon Simple Storage Service (Amazon S3) to minimize latency and cost.

Rationale: AWS CloudFormation is an infrastructure automation tool, not a content delivery network or hosting service. It cannot reduce latency for end users or automate global content delivery for static content.



Question 34
You are the solutions architect for a social media website that uses an Amazon DynamoDB table on the backend. Monitoring reveals that the table begins to throttle requests during peak load, which is slowing down the application. You have been asked to address the throttling, improve performance, and reduce operational complexity. What should you do?

Correct Answers
Selected
Use Amazon DynamoDB auto scaling.

Rationale: Amazon DynamoDB auto scaling automatically manages read and write capacity to match traffic, fixes throttling, and reduces operational complexity by removing the need for manual scaling adjustments.

Incorrect Answers
Put the DynamoDB table behind an Auto Scaling group.

Rationale: Amazon EC2 Auto Scaling groups manage EC2 instances, not DynamoDB capacity; placing tables behind one does not affect DynamoDB throughput or simplify operations.

Migrate the database to Amazon Relational Database Service (Amazon RDS) for MySQL with Multi-AZ.

Rationale: Migrating to Amazon Relational Database Service (Amazon RDS) for MySQL would not fix DynamoDB throttling and increases operational complexity by switching database types and management models.

Create an Amazon Aurora read replica and spread the load between DynamoDB and Aurora.

Rationale: Aurora read replicas are used for read scaling within Aurora clusters. Spreading load between DynamoDB and Aurora is not technically feasible or supported.



Question 35
You are the solutions architect for an online booking system for vacations. The system uses Amazon Elastic Compute Cloud (EC2) instances on the frontend to poll an Amazon Simple Queue Service (SQS) queue. You have discovered that some bookings are being processed twice, causing customers to pay multiple times for the same reservation. This is creating significant problems for your customer service team. What should you do to prevent this issue from happening in the future?

Correct Answers
Use an Amazon Simple Queue Service (SQS) FIFO queue instead.

Rationale: FIFO queues support exactly-once processing and message deduplication with a five-minute dedupe window, eliminating duplicate message delivery and solving double processing issues.

Incorrect Answers
Replace SQS with Amazon Simple Workflow Service (SWF).

Rationale: Amazon Simple Workflow Service (SWF) is designed for complex workflow management; it does not prevent duplicate messages in the same way as FIFO SQS and may involve re-architecting the application.

Change the message size in Amazon Simple Queue Service (SQS).

Rationale: The message size is related to the amount of data that can be sent in a single message. Changing the message size doesn't address the issue of duplicate processing but can be relevant if you need to ensure that your messages can accommodate all necessary data.

Selected
Alter the visibility timeout of Amazon Simple Queue Service (SQS).

Rationale: The visibility timeout determines how long a message remains invisible in the queue after a worker starts processing it. Changing the visibility timeout can help in some scenarios, but it won't completely prevent duplicate processing. It's more about giving your workers additional time to process messages without them becoming visible to other workers.



Question 37
A company has an Auto Scaling group of Amazon Elastic Compute Cloud (EC2) instances hosting its retail sales application. Any significant downtime can result in large profit losses. The architecture includes an Application Load Balancer and an Amazon Relational Database Service (Amazon RDS) database in a Multi-AZ deployment. The company has an aggressive Recovery Time Objective (RTO) for disaster recovery. How long does an Amazon RDS Multi-AZ failover typically take to complete?

Correct Answers
One to two minutes.

Rationale: Amazon Relational Database Service (Amazon RDS) Multi-AZ failovers typically complete within 60 to 120 seconds. This is standard for Multi-AZ deployments and aligns with AWS documentation and typical RTO planning.

Incorrect Answers
Almost instantly.

Rationale: Failover is not instantaneous. There is always some delay due to DNS propagation, connection draining, and promotion of the standby instance, so it cannot be considered immediate.

Within an hour.

Rationale: Multi-AZ failovers are designed for high availability and typically finish within a few minutes, not up to an hour, which would be considered unacceptable for most production applications.

Selected
Under 10 minutes.

Rationale: While accurate that failover is often under 10 minutes, AWS documentation and real-world measurements show the process usually takes significantly less time.



Question 41
You are a solutions architect working for a biotech company that has a large private cloud deployment using VMware. You have been tasked to set up a disaster recovery solution on AWS. What is the simplest way to achieve this?

Correct Answers
Selected
Purchase VMware Cloud on AWS, leveraging VMware disaster recovery technologies and the speed of AWS cloud to protect your virtual machines.

Rationale: VMware Cloud on AWS is a managed service jointly engineered by AWS and VMware, enabling seamless integration of on-premises VMware workloads with AWS infrastructure. It supports built-in VMware disaster recovery tools, simplifies operations, and eliminates the need for custom EC2 or manual vCenter deployments.

Incorrect Answers
Deploy an Amazon Elastic Compute Cloud (EC2) instance into a private subnet and install VMware vCenter on it.

Rationale: Manually installing vCenter on a single EC2 instance does not provide an integrated, supported, or scalable solution. This approach adds complexity and lacks redundancy, manageability, and vendor support for disaster recovery.

Use the VMware landing page on AWS to provision an EC2 instance with VMware vCenter installed on it.

Rationale: There is no official AWS or VMware landing page or automated method to directly provision EC2 with vCenter pre-installed as a DR solution. Disaster recovery still requires proper integration with VMware Cloud on AWS or equivalent service.

Deploy an Amazon Elastic Compute Cloud (EC2) instance into a public subnet and install VMware vCenter on it.

Rationale: Placing vCenter in a public subnet increases security risks and does not provide integration with AWS-managed DR capabilities. This method is not recommended, not managed, and is operationally complex.



Question 44
You are working as a solutions architect for an online travel company. Your application is going to use an Auto Scaling group of Amazon Elastic Compute Cloud (EC2) instances, but you need to decouple components and store messages due to high traffic volume. Which AWS service can you add to meet this requirement?

Correct Answers
Selected
Implement Amazon Simple Queue Service (Amazon SQS) for message storage during high-volume traffic.

Rationale: Amazon Simple Queue Service (Amazon SQS) is a fully managed message queue service designed for decoupling and buffering communications in distributed, auto-scaled applications. It is reliable, cost-effective, scalable, and purpose-built for asynchronous message storage and processing.

Incorrect Answers
Implement Amazon ElastiCache as a storage location for messages when high volumes of traffic are present.

Rationale: Amazon ElastiCache is an in-memory cache solution, not a message queue. While it can temporarily buffer data, it is not designed for durable message storage or decoupled asynchronous processing in autoscaled environments.

Configure Amazon Relational Database Service (Amazon RDS) read replicas as a storage location for messages during high volumes of traffic.

Rationale: Amazon RDS read replicas provide read scalability for relational databases but are not designed as a message buffering or queueing solution. Using them for message queuing is not maintainable or efficient at high scale.

Implement Amazon Simple Workflow Service (Amazon SWF), which initiates an AWS Lambda function to process the messages during high volume traffic loads.

Rationale: Amazon Simple Workflow Service (Amazon SWF) is an orchestration service for managing stateful, long-running workflows. It is not a simple message buffer or decoupling mechanism for high-volume transactional message ingestion.


Question 45
You are restructuring your infrastructure to enhance the resilience of your web application by decoupling its components. To achieve precise, once-only processing and maintain message order, which type of Amazon Simple Queue Service (SQS) queue should you select?

Correct Answers
Selected
Amazon SQS FIFO queue

Rationale: FIFO (First-In-First-Out) queues delivers messages exactly once and in the precise order in which they were sent, meeting requirements for exactly-once processing and strict message.

Incorrect Answers
Amazon SQS standard queue

Rationale: A standard queue offers at-least-once delivery and best-effort ordering, so it can deliver duplicates and does not guarantee message order.

Amazon SQS dead-letter queue

Rationale: Amazon SQS supports dead-letter queues (DLQ), which other queues (source queues) can target for messages that can't be processed (consumed) successfully. It is not suitable to allow your messages to be processed exactly once and in order.

Amazon SQS LIFO queue

Rationale: There is no such feature as an Amazon SQS LIFO (Last in First Out) queue. SQS only offers standard and FIFO queues


Question 54
You have a website running on an Amazon Elastic Compute Cloud (EC2) instance. The website is a static HTML site and does not require a database connection. After the site goes viral, the EC2 instance fails under the increased load. You need to ensure that service outages like this do not recur. Which architecture provides the best resiliency?

Correct Answers
Selected
Host the static website on Amazon Simple Storage Service (Amazon S3).

Rationale: Amazon Simple Storage Service (Amazon S3) provides virtually unlimited scale, built-in high availability, and resilience. S3 static website hosting can handle viral traffic without requiring server management or scaling.

Incorrect Answers
Increase the size of the Amazon Elastic Compute Cloud (EC2) instance so it can cope with the load.

Rationale: Upgrading an instance only temporarily boosts capacity. It still leaves a single point of failure and finite scalability, so viral events can lead to another outage.

Migrate the website to AWS CloudFormation.

Rationale: AWS CloudFormation is an infrastructure-as-code tool for provisioning resources, not a hosting service. It does not deliver resiliency by itself or solve scaling challenges for static sites.

Add another Amazon Elastic Compute Cloud (EC2) instance in the same availability zone and place the two instances behind an application load balancer.

Rationale: Adding another instance with a load balancer improves availability, but hosting static content on EC2 remains less resilient and less scalable than using Amazon S3. True resiliency requires eliminating compute/server dependencies.
