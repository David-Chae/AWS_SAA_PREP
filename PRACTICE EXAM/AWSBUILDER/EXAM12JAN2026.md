Q3.
A company needs to look up configuration details about how a Linux-based Amazon EC2 instance was launched.
Which command should a solutions architect run on the EC2 instance to gather the system metadata?

A
curl http://169.254.169.254/latest/meta-data/

Correct. The only way to retrieve instance metadata is to use the link-local address, which is 169.254.169.254.

For more information about instance metadata, see Retrieve Instance Metadata.


B (SELECTED)
curl http://localhost/latest/meta-data/

Incorrect. The use of localhost will not work because this solution checks an IP address of 127.0.0.1. Metadata is not available through the use of the localhost name.


C
curl http://254.169.254.169/latest/meta-data/

Incorrect. The format for the link-local address is 169.254.169.254.


D
curl http://192.168.0.1/latest/meta-data/

Incorrect. Instance metadata is not available through 192.168.x.x.


Q4.
A company is transitioning its Amazon EC2 based MariaDB database to Amazon RDS. The company has already identified a database instance type that will meet the company's CPU and memory requirements. The database must provide at least 40 GiB of storage capacity and 1,000 IOPS.
Which storage configuration for the Amazon RDS for MariaDB instance is MOST cost-effective?

A
Provision 350 GiB of magnetic storage for the RDS instance.

Incorrect. Magnetic storage does not support IOPS as a configurable parameter.

For more information about magnetic storage, see Amazon RDS Storage Types.


B
Provision 50 GiB of General Purpose SSD (gp3) storage for the RDS instance.

Correct. General Purpose SSD (gp3) includes 3,000 IOPS at no additional cost independent of volume size.

For more information about EBS pricing, see Amazon EBS Pricing.

For more information about General Purpose SSD storage, see General Purpose SSD Storage.


C
Provision 334 GiB of General Purpose SSD (gp2) storage for the RDS instance.

Incorrect. General Purpose SSD (gp2) IOPS are dependent on volume size at a rate of 3 IOPS/GB. Provisioning 334 GiB of storage on gp2 to achieve the required IOPS would be more expensive than using 50 GiB of gp3.

For more information about EBS volume types, see Amazon EBS Volume Types.

For more information about EBS pricing, see Amazon EBS Pricing.


D (SELECTED)
Provision 50 GiB of Provisioned IOPS storage with 1,000 IOPS for the RDS instance.

Incorrect. 50 GiB of Provisioned IOPS storage with 1,000 IOPS would be more expensive than 50 GiB of General Purpose SSD (gp3) storage.


Q11.
A media company is designing a new application for graphic rendering. The application requires up to 400 GB of storage for temporary data that is discarded after the frames are rendered. The application requires approximately 40,000 random IOPS to perform the rendering.
What is the MOST cost-effective storage option for this rendering application?

A
A storage optimized Amazon EC2 instance with instance store storage

Correct. Storage optimized instances are designed for workloads that require high, sequential read and write access to very large datasets on local storage. These instances are optimized to provide applications with tens of thousands of low-latency, random IOPS. The instance store has no additional cost.

For more information about storage optimized instances, see Storage Optimized Instances.

For more information about instance stores, see Amazon EC2 Instance Store.


B (Selected)
A storage optimized Amazon EC2 instance with a Provisioned IOPS SSD (io1 or io2) Amazon Elastic Block Store (Amazon EBS) volume

Incorrect. Provisioned IOPS SSD (io1 or io2) EBS volumes can deliver more than the 40,000 IOPS that are required in the scenario. However, this solution is not as cost-effective as an instance store because Amazon EBS adds cost to the hourly instance rate. This solution provides persistence of data beyond the lifecycle of the instance, but persistence is not required in this use case.

For more information about Provisioned IOPS SSD (io1 or io2) EBS volumes, see Provisioned IOPS SSD Volumes.

For more information about pricing for Amazon EBS, see Amazon EBS Pricing.


C
A burstable Amazon EC2 instance with a Throughput Optimized HDD (st1) Amazon Elastic Block Store (Amazon EBS) volume

Incorrect. Throughput Optimized HDD (st1) EBS volumes are engineered to maximize the throughput of data that can be sent to and from a volume, not the random IOPS. Consequently, this solution does not meet the IOPS requirement. Additionally, Amazon EBS adds cost to the hourly instance rate. This solution provides persistence of data beyond the lifecycle of the instance, but persistence is not required in this use case.

For more information about Throughput Optimized HDD (st1) EBS volumes, see Throughput Optimized HDD and Cold HDD Volumes.

For more information about pricing for Amazon EBS, see Amazon EBS Pricing.


D
A burstable Amazon EC2 instance with Amazon S3 storage over a VPC endpoint

Incorrect. Amazon S3 (object storage) is not the most suitable solution for rapidly changing data that is required for the scratch volume space. Block storage is appropriate for the read/write functionality to work smoothly.

For more information about usage patterns for Amazon S3, see Performance Design Patterns for Amazon S3.


Q13.
A company needs to maintain data records for a minimum of 5 years. The data is rarely accessed after it is stored. The data must be accessible within 2 hours.
Which solution will meet these requirements MOST cost-effectively?

A
Store the data in an Amazon Elastic File System (Amazon EFS) file system. Access the data by using AWS Direct Connect.

Incorrect. This solution is not the most cost-effective solution. Amazon S3 is a more cost-effective solution if there is not a requirement for a file system.

For more information about Amazon EFS and Direct Connect, see How Amazon EFS works with AWS Direct Connect and AWS Managed VPN.


B
Store the data in an Amazon Elastic Block Store (Amazon EBS) volume. Create snapshots. Store the snapshots in an Amazon S3 bucket.

Incorrect. This solution is not the most cost-effective solution because it requires the use of Amazon EBS in addition to Amazon S3.

For more information about EBS snapshots, see Amazon EBS snapshots.


C (Selected)
Store the data in an Amazon S3 bucket. Use an S3 Lifecycle policy to move the data to S3 Standard-Infrequent Access (S3 Standard-IA).

Incorrect. The storage of the data in an S3 bucket provides a cost-effective initial location for the data. However, S3 Standard-IA is not the most cost-effective storage class to meet the requirements in the scenario. The S3 Glacier storage class is designed for low-cost data archiving.

For more information about S3 storage classes, see Using Amazon S3 storage classes.


D 
Store the data in an Amazon S3 bucket. Use an S3 Lifecycle policy to move the data to S3 Glacier Instant Retrieval.

Correct. The storage of the data in an S3 bucket provides a cost-effective initial location for the data. S3 Glacier Instant Retrieval is the most cost-effective archival storage solution that meets the requirement of a 2-hour retrieval time.

For more information about how to move data between S3 storage classes automatically, see Managing your storage lifecycle.

For more information about S3 storage classes, see Using Amazon S3 storage classes.


Q16.
A company has strict data protection requirements. A solutions architect must configure security for a VPC to ensure that backend Amazon RDS DB instances cannot be accessed from the internet. The solutions architect must ensure that the DB instances are accessible from the application tier over a specified port only.
Which actions should the solutions architect take to meet these requirements? (Select TWO.)

A
Specify a DB subnet group that contains only private subnets for the DB instances.

Correct. A private subnet is one component to use to secure the database tier. Internet traffic is not routed to a private subnet. When you place DB instances in a private subnet, you add a layer of security.

For more information about VPCs with public subnets and private subnets, see Routing.


B
Attach an elastic network interface with a private IPv4 address to each DB instance.

Incorrect. An elastic network interface is a logical networking component in a VPC that represents a virtual network card. The use of an elastic network interface would not meet the requirements in the scenario.

For more information about elastic network interfaces, see Elastic network interfaces.


C (Selected)
Configure AWS Shield with the VPC. Update the route tables for the subnets that the DB instances use.

Incorrect. Shield provides protection against DDoS attacks. Shield cannot be a target of routes in a route table. The use of Shield would not meet the requirements in the scenario.

For more information about Shield, see AWS Shield.


D
Configure an AWS Direct Connect connection on the database port between the application tier and the backend.

Incorrect. Direct Connect provides a dedicated connection to your AWS environment. The use of Direct Connect would not meet the requirements in the scenario.

For more information about Direct Connect, see AWS Direct Connect features.


E (Selected)
Add an inbound rule to the database security group that allows requests from the security group of the application tier over the database port. Remove other inbound rules.

Correct. Security groups can restrict access to the DB instances. Security groups provide access from only the application tier on only a specific port.

For more information about security groups, see Security group basics.


Q18. 
A reporting application runs on Amazon EC2 instances behind an Application Load Balancer. The instances run in an Amazon EC2 Auto Scaling group across multiple Availability Zones. For complex reports, the application can take up to 15 minutes to respond to a request. A solutions architect is concerned that users will receive HTTP 5xx errors if a report request is in process during a scale-in event.
What should the solutions architect do to ensure that user requests will be completed before instances are terminated?

A (Selected)
Enable sticky sessions (session affinity) for the target group of the instances.

Incorrect. If an EC2 instance were removed from the target group during a scale-in process, the EC2 instance would fail (or would be unhealthy if it were checked). An Application Load Balancer would stop routing requests to that target and would choose a new healthy target.

For more information about sticky sessions, see Sticky Sessions for Your Application Load Balancer.


B
Increase the instance size in the Application Load Balancer target group.

Incorrect. An increase of the instance size likely would increase the speed of processing. However, this solution does not directly ensure that instances that process a request are unaffected by scale-in actions. A more suitable solution would be to use deregistration delay.

For more information about deregistration delay, see Deregistration Delay.


C
Increase the cooldown period for the Auto Scaling group to a greater amount of time than the time required for the longest running responses.

Incorrect. Amazon EC2 Auto Scaling cooldown periods help you prevent Auto Scaling groups from launching or terminating additional instances before the effects of previous activities are apparent.

For more information about cooldown periods, see Scaling Cooldowns for Amazon EC2 Auto Scaling.


D
Increase the deregistration delay timeout for the target group of the instances to greater than 900 seconds.

Correct. By default, the Application Load Balancer waits 300 seconds before the completion of the deregistration process, which can help in-flight requests to the target become complete. To change the amount of time that the Application Load Balancer waits, update the deregistration delay value.

For more information about deregistration delay, see Deregistration Delay.


Q20. 
A company asks a solutions architect to implement a pilot light disaster recovery (DR) strategy for an existing on-premises application. The application is self contained and does not need to access any databases.

Which solution will implement a pilot light DR strategy?


A (Selected)
Back up the on-premises application, configuration, and data to an Amazon S3 bucket. When the on-premises application fails, build a new hosting environment on AWS and restore the application from the information that is stored in the S3 bucket.

Incorrect. This is a backup and restore DR strategy. Backup and restore DR strategies typically have the lowest cost but highest recovery time. A solution that manually rebuilds the hosting infrastructure on AWS could take hours.


B
Recreate the application hosting environment on AWS by using Amazon EC2 instances and stop the EC2 instances. When the on-premises application fails, start the stopped EC2 instances and direct 100% of application traffic to the EC2 instances that are running in the AWS Cloud.

Correct. This is a pilot light DR strategy. This solution recreates an existing application hosting environment in an AWS Region. This solution turns off most (or all) resources and uses the resources only during tests or when DR failover is necessary. RPO and RTO are usually 10s of minutes.

A pilot light strategy simplifies recovery at the time of a disaster because the core infrastructure requirements are all in place. A pilot light strategy also minimizes the ongoing cost of DR by minimizing the active resources.

For more information about the pilot light DR strategies, see Disaster Recovery Options in the Cloud.


C
Recreate the application hosting environment on AWS by using Amazon EC2 instances. Direct 10% of application traffic to the EC2 instances that are running in the AWS Cloud. When the on-premises application fails, direct 100% of application traffic to the EC2 instances that are running in the AWS Cloud.

Incorrect. This is a warm standby DR strategy. This solution recreates an existing application hosting environment in an AWS Region. This solution serves a portion of live traffic. With this DR strategy, RPO and RTO are usually a few minutes. However, costs are higher because this solutions runs resources continuously.


D
Back up the on-premises application, configuration, and data to an Amazon S3 bucket. When the on-premises application fails, rebuild the on-premises hosting environment and restore the application from the information that is stored in the S3 bucket.

Incorrect. This is a backup and restore DR strategy. Backup and restore DR strategies typically have the lowest cost but highest recovery time. A solution that manually rebuilds the hosting infrastructure on premises and downloads the data that a company has backed up could take hours or days.
