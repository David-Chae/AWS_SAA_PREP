1. Question
A company is running a dashboard application on a Spot EC2 instance inside a private subnet. The dashboard is reachable via a domain name that maps to the private IPv4 address of the instance’s network interface. A solutions architect needs to increase network availability by allowing the traffic flow to resume in another instance if the primary instance is terminated.

Which solution accomplishes these requirements?

1. Create a secondary elastic network interface and point its private IPv4 address to the application’s domain name. Attach the new network interface to the primary instance. If the instance goes down, move the secondary network interface to another instance.
2. Attach an elastic IP address to the instance’s primary network interface and point its IP address to the application’s domain name. Automatically move the EIP to a secondary instance if the primary instance becomes unavailable using the AWS Transit Gateway.
3. Use the AWS Network Firewall to detach the instance’s primary elastic network interface and move it to a new instance upon failure.
4. Set up AWS Transfer for FTPS service in Implicit FTPS mode to automatically disable the source/destination checks on the instance’s primary elastic network interface and reassociate it to another instance.

Incorrect
If one of your instances serving a particular function fails, its network interface can be attached to a replacement or hot standby instance pre-configured for the same role in order to rapidly recover the service. For example, you can use a network interface as your primary or secondary network interface to a critical service such as a database instance or a NAT instance. If the instance fails, you (or more likely, the code running on your behalf) can attach the network interface to a hot standby instance.

Because the interface maintains its private IP addresses, Elastic IP addresses, and MAC address, network traffic begins flowing to the standby instance as soon as you attach the network interface to the replacement instance. Users experience a brief loss of connectivity between the time the instance fails and the time that the network interface is attached to the standby instance, but no changes to the route table or your DNS server are required.

Hence, the correct answer is Create a secondary elastic network interface and point its private IPv4 address to the application’s domain name. Attach the new network interface to the primary instance. If the instance goes down, move the secondary network interface to another instance.

The option that says: Attach an elastic IP address to the instance’s primary network interface and point its IP address to the application’s domain name. Automatically move the EIP to a secondary instance if the primary instance becomes unavailable using the AWS Transit Gateway is incorrect. Elastic IPs are not needed in the solution since the application is private. Furthermore, an AWS Transit Gateway is primarily used to connect your Amazon Virtual Private Clouds (VPCs) and on-premises networks through a central hub. This particular networking service cannot be used to automatically move an Elastic IP address to another EC2 instance.

The option that says: Set up AWS Transfer for FTPS service in Implicit FTPS mode to automatically disable the source/destination checks on the instance’s primary elastic network interface and reassociate it to another instance is incorrect. First of all, the AWS Transfer for FTPS service is not capable of automatically disabling the source/destination checks and it only supports Explicit FTPS mode. Disabling the source/destination check only allows the instance to which the ENI is connected to act as a gateway (both a sender and a receiver). It is not possible to make the primary ENI of any EC2 instance detachable. A more appropriate solution would be to use an Elastic IP address which can be reassociated with your secondary instance.

The option that says: Use the AWS Network Firewall to detach the instance’s primary elastic network interface and move it to a new instance upon failure is incorrect. It’s not possible to detach the primary network interface of an EC2 instance. In addition, the AWS Network Firewall is only used for filtering traffic at the perimeter of your VPC and not for detaching ENIs.


References:
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/scenarios-enis.html
https://aws.amazon.com/aws-transfer-family/faqs/





2. Question
The media company that you are working for has a video transcoding application running on Amazon EC2. Each EC2 instance polls a queue to find out which video should be transcoded, and then runs a transcoding process. If this process is interrupted, the video will be transcoded by another instance based on the queuing system. This application has a large backlog of videos which need to be transcoded. Your manager would like to reduce this backlog by adding more EC2 instances, however, these instances are only needed until the backlog is reduced.
In this scenario, which type of Amazon EC2 instance is the most cost-effective type to use?

Reserved instances
Spot instances
Dedicated instances
On-demand instances (SELECTED)

Incorrect
You require an instance that will be used not as a primary server but as a spare compute resource to augment the transcoding process of your application. These instances should also be terminated once the backlog has been significantly reduced. In addition, the scenario mentions that if the current process is interrupted, the video can be transcoded by another instance based on the queuing system. This means that the application can gracefully handle an unexpected termination of an EC2 instance, like in the event of a Spot instance termination when the Spot price is greater than your set maximum price. Hence, an Amazon EC2 Spot instance is the best and cost-effective option for this scenario.
Amazon EC2 Spot instances are spare compute capacity in the AWS cloud available to you at steep discounts compared to On-Demand prices. EC2 Spot enables you to optimize your costs on the AWS cloud and scale your application’s throughput up to 10X for the same budget. By simply selecting Spot when launching EC2 instances, you can save up to 90% on On-Demand prices. The only difference between On-Demand instances and Spot Instances is that Spot instances can be interrupted by EC2 with two minutes of notification when the EC2 needs the capacity back.
You can specify whether Amazon EC2 should hibernate, stop, or terminate Spot Instances when they are interrupted. You can choose the interruption behavior that meets your needs.
Take note that there is no “bid price” anymore for Spot EC2 instances since March 2018. You simply have to set your maximum price instead.
Reserved instances and Dedicated instances are incorrect as both do not act as spare compute capacity.
On-demand instances is a valid option but a Spot instance is much cheaper than On-Demand.
 

References: 
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-interruptions.html
http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/how-spot-instances-work.html
https://aws.amazon.com/blogs/compute/new-amazon-ec2-spot-pricing

Check out this Amazon EC2 Cheat Sheet:
https://tutorialsdojo.com/amazon-elastic-compute-cloud-amazon-ec2/

Check out this Amazon EC2 Cheat Sheet:
https://tutorialsdojo.com/amazon-elastic-compute-cloud-amazon-ec2/




4. Question
There was an incident in a production environment where user data stored in an Amazon S3 bucket was accidentally deleted by a Junior DevOps Engineer. The issue was escalated to management, and after a few days, an instruction was given to improve the security and protection of AWS resources.

What combination of the following options will protect the S3 objects in the bucket from both accidental deletion and overwriting? (Select TWO.)

Disallow S3 Delete using an IAM bucket policy
Enable Versioning
Enable S3 Intelligent-Tiering
Enable Multi-Factor Authentication Delete
Provide access to S3 data strictly through pre-signed URL only

Incorrect
By using Versioning and enabling MFA (Multi-Factor Authentication) Delete, you can secure and recover your S3 objects from accidental deletion or overwrite.

S3 Bucket Versioning

Versioning is a means of keeping multiple variants of an object in the same bucket. Versioning-enabled buckets enable you to recover objects from accidental deletion or overwrite. You can use versioning to preserve, retrieve, and restore every version of every object stored in your Amazon S3 bucket. With versioning, you can easily recover from both unintended user actions and application failures.

S3 Enable MFA

You can also optionally add another layer of security by configuring a bucket to enable MFA (Multi-Factor Authentication) Delete, which requires additional authentication for either of the following operations:

– Change the versioning state of your bucket

– Permanently delete an object version

MFA Delete requires two forms of authentication together:

– Your security credentials

– The concatenation of a valid serial number, a space, and the six-digit code displayed on an approved authentication device.

 

Hence, the correct answers are:
– Enable Versioning
– Enable Multi-Factor Authentication Delete
The option that says: Providing access to S3 data strictly through pre-signed URL only is incorrect since a pre-signed URL gives access to the object identified in the URL. Pre-signed URLs are useful when customers perform an object upload to your S3 bucket, but does not help in preventing accidental deletes.
The option that says: Disallowing S3 Delete using an IAM bucket policy is incorrect since you still want users to be able to delete objects in the bucket, and you just want to prevent accidental deletions. Disallowing S3 Delete using an IAM bucket policy will restrict all delete operations to your bucket.
The option that says: Enabling S3 Intelligent-Tiering is incorrect since S3 intelligent tiering does not help in this situation.

 

References:
https://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html
https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html

Check out this Amazon S3 Cheat Sheet:
https://tutorialsdojo.com/amazon-s3/




5. Question
A Solutions Architect working for a startup is designing a High Performance Computing (HPC) application which is publicly accessible for their customers. The startup founders want to mitigate distributed denial-of-service (DDoS) attacks on their application.

Which of the following options are not suitable to be implemented in this scenario? (Select TWO.)

Use Dedicated EC2 instances to ensure that each instance has the maximum performance possible.
Use an Amazon CloudFront service for distributing both static and dynamic content.
Add multiple Elastic Fabric Adapters (EFA) to each EC2 instance to increase the network bandwidth.
Use an Application Load Balancer with Auto Scaling groups for your EC2 instances. Prevent direct Internet traffic to your Amazon RDS database by deploying it to a new private subnet.
Use AWS Shield and AWS WAF.
Incorrect
Take note that the question asks about the viable mitigation techniques that are NOT suitable to prevent Distributed Denial of Service (DDoS) attack.

A Denial of Service (DoS) attack is an attack that can make your website or application unavailable to end users. To achieve this, attackers use a variety of techniques that consume network or other resources, disrupting access for legitimate end users.

To protect your system from DDoS attack, you can do the following:

– Use an Amazon CloudFront service for distributing both static and dynamic content.

– Use an Application Load Balancer with Auto Scaling groups for your EC2 instances. Prevent direct Internet traffic to your Amazon RDS database by deploying it to a new private subnet.

– Set up alerts in Amazon CloudWatch to look for high Network In and CPU utilization metrics.

Services that are available within AWS Regions, like Elastic Load Balancing and Amazon Elastic Compute Cloud (EC2), allow you to build Distributed Denial of Service resiliency and scale to handle unexpected volumes of traffic within a given region. Services that are available in AWS edge locations, like Amazon CloudFront, AWS WAF, Amazon Route53, and Amazon API Gateway, allow you to take advantage of a global network of edge locations that can provide your application with greater fault tolerance and increased scale for managing larger volumes of traffic.

In addition, you can also use AWS Shield and AWS WAF to fortify your cloud network. AWS Shield is a managed DDoS protection service that is available in two tiers: Standard and Advanced. AWS Shield Standard applies always-on detection and inline mitigation techniques, such as deterministic packet filtering and priority-based traffic shaping, to minimize application downtime and latency.

AWS WAF is a web application firewall that helps protect web applications from common web exploits that could affect application availability, compromise security, or consume excessive resources. You can use AWS WAF to define customizable web security rules that control which traffic accesses your web applications. If you use AWS Shield Advanced, you can use AWS WAF at no extra cost for those protected resources and can engage the DRT to create WAF rules.



Using Dedicated EC2 instances to ensure that each instance has the maximum performance possible is not a viable mitigation technique because Dedicated EC2 instances are just an instance billing option. Although it may ensure that each instance gives the maximum performance, that by itself is not enough to mitigate a DDoS attack.

Adding multiple Elastic Fabric Adapters (EFA) to each EC2 instance to increase the network bandwidth is also not a viable option as this is mainly done for performance improvement and not for DDoS attack mitigation. Moreover, you can attach only one EFA per EC2 instance. An Elastic Fabric Adapter (EFA) is a network device that you can attach to your Amazon EC2 instance to accelerate High-Performance Computing (HPC) and machine learning applications.

The following options are valid mitigation techniques that can be used to prevent DDoS:

– Use an Amazon CloudFront service for distributing both static and dynamic content.

– Use an Application Load Balancer with Auto Scaling groups for your EC2 instances. Prevent direct Internet traffic to your Amazon RDS database by deploying it to a new private subnet.

– Use AWS Shield and AWS WAF.

 

References:

https://aws.amazon.com/answers/networking/aws-ddos-attack-mitigation/

https://d0.awsstatic.com/whitepapers/DDoS_White_Paper_June2015.pdf

 

Best practices on DDoS Attack Mitigation:



7. Question
A financial application consists of an Auto Scaling group of Amazon EC2 instances, an Application Load Balancer, and a MySQL RDS instance set up in a Multi-AZ Deployment configuration. To protect customers’ confidential data, it must be ensured that the Amazon RDS database is only accessible using an authentication token specific to the profile credentials of EC2 instances.

Which of the following actions should be taken to meet this requirement?

Configure SSL in your application to encrypt the database connection to RDS.
Create an IAM Role and assign it to your EC2 instances which will grant exclusive access to your RDS instance.
Use a combination of IAM and STS to enforce restricted access to your RDS instance using a temporary authentication token.
Enable the IAM DB Authentication.
Incorrect
You can authenticate to your DB instance using AWS Identity and Access Management (IAM) database authentication. IAM database authentication works with MySQL and PostgreSQL. With this authentication method, you don’t need to use a password when you connect to a DB instance. Instead, you use an authentication token.

An authentication token is a unique string of characters that Amazon RDS generates on request. Authentication tokens are generated using AWS Signature Version 4. Each token has a lifetime of 15 minutes. You don’t need to store user credentials in the database, because authentication is managed externally using IAM. You can also still use standard database authentication.

IAM database authentication

IAM database authentication provides the following benefits:

Network traffic to and from the database is encrypted using Secure Sockets Layer (SSL).
You can use IAM to centrally manage access to your database resources, instead of managing access individually on each DB instance.
For applications running on Amazon EC2, you can use profile credentials specific to your EC2 instance to access your database instead of a password, for greater security
Hence, the correct answer is: Enable the IAM DB Authentication.

The option that says: Configuring SSL in your application to encrypt the database connection to RDS is incorrect because an SSL connection is not just using an authentication token from IAM. Although configuring SSL to your application can improve the security of your data in flight, it is still not a suitable option to use in this scenario.

The option that says: Creating an IAM Role and assigning it to your EC2 instances which will grant exclusive access to your RDS instance is incorrect because although you can create and assign an IAM Role to your EC2 instances, you still need to configure your RDS to use IAM DB Authentication.

The option that says: Use a combination of IAM and STS to enforce restricted access to your RDS instance using a temporary authentication token is incorrect because you have to use IAM DB Authentication for this scenario, and not simply a combination of an IAM and STS. Although STS is used to send temporary tokens for authentication, this is not a compatible use case for RDS.

 

References:

https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.IAMDBAuth.html

https://aws.amazon.com/rds/ 

 

Check out this Amazon RDS cheat sheet:

https://tutorialsdojo.com/amazon-relational-database-service-amazon-rds/





11. Question
A company is building an automation tool for generating custom reports on its AWS usage. The company must be able to programmatically access and forecast usage costs on specific services.

Which of the following would meet the requirements with the LEAST amount of operational overhead?

Configure AWS Budgets to send usage cost data to the company via Amazon SNS.
Use the AWS Cost Explorer API with pagination to programmatically retrieve the usage cost-related data.
Utilize the downloadable AWS Cost Explorer report .csv files to access the cost-related data. Predict usage costs using AWS Budgets.
Generate AWS Budgets reports for usage cost data and deliver them via Amazon Simple Queue Service (SQS).
Incorrect
AWS Cost Explorer is a service provided by Amazon Web Services (AWS) that helps you visualize, understand, and analyze your AWS costs and usage. It provides a comprehensive set of tools and features to help you monitor and manage your AWS spending.



The primary purpose of AWS Cost Explorer is to help you gain insights into your AWS costs and usage patterns over time. It lets you view and analyze your historical spending data, forecast future costs, and identify cost-saving opportunities.

You can programmatically query your cost and usage data via the Cost Explorer API. You can query for aggregated data such as total monthly costs or total daily usage. You can also query for granular data, such as the number of daily write operations for DynamoDB database tables in your production environment.

By using the AWS Cost Explorer API, the company can programmatically access the usage cost-related data they need on specific services. The pagination feature allows for the efficient retrieval of large datasets.

Hence the correct answer is: Use the AWS Cost Explorer API with pagination to programmatically retrieve the usage cost-related data.

The option that says: Utilize the downloadable AWS Cost Explorer report .csv files to access the cost-related data. Predict usage costs using AWS Budgets is incorrect. This option involves the process of manually downloading .csv files, which adds significant operational overhead compared to directly accessing data through the AWS Cost Explorer API. This method simply lacks the ability to programmatically and dynamically retrieve usage data, making it a less efficient solution.

The option that says: Configure AWS Budgets to send usage cost data to the company via Amazon SNS is incorrect because this simply helps you get notified on budget thresholds; it does not provide access to the usage of cost-related data.

The option that says: Generate AWS Budgets reports for usage cost data and deliver them via Amazon Simple Queue Service (SQS) is incorrect. AWS Budgets just allows you to set custom cost and usage budgets that alert you when your budget thresholds are exceeded. It won’t give you detailed information on AWS usage and cost.

 

References:

https://docs.aws.amazon.com/cost-management/latest/userguide/ce-what-is.html

https://docs.aws.amazon.com/cost-management/latest/userguide/ce-api.html

 

Check out this AWS Billing and Cost Management Cheat Sheet:

https://tutorialsdojo.com/aws-billing-and-cost-management/






14. Question
A company hosted a web application in an Auto Scaling group of EC2 instances. The IT manager is concerned about the over-provisioning of the resources that can cause higher operating costs. A Solutions Architect has been instructed to create a cost-effective solution without affecting the performance of the application.

Which dynamic scaling policy should be used to satisfy this requirement?

Use simple scaling.
Use scheduled scaling.
Use suspend and resume scaling.
Use target tracking scaling.
Incorrect
An Auto Scaling group contains a collection of Amazon EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management. An Auto Scaling group also enables you to use Amazon EC2 Auto Scaling features such as health check replacements and scaling policies. Both maintaining the number of instances in an Auto Scaling group and automatic scaling are the core functionality of the Amazon EC2 Auto Scaling service. The size of an Auto Scaling group depends on the number of instances that you set as the desired capacity. You can adjust its size to meet demand, either manually or by using automatic scaling.

Step scaling policies and simple scaling policies are two of the dynamic scaling options available for you to use. Both require you to create CloudWatch alarms for the scaling policies. Both require you to specify the high and low thresholds for the alarms. Both require you to define whether to add or remove instances, and how many, or set the group to an exact size. The main difference between the policy types is the step adjustments that you get with step scaling policies. When step adjustments are applied, and they increase or decrease the current capacity of your Auto Scaling group, the adjustments vary based on the size of the alarm breach.



The primary issue with simple scaling is that after a scaling activity is started, the policy must wait for the scaling activity or health check replacement to complete and the cooldown period to expire before responding to additional alarms. Cooldown periods help to prevent the initiation of additional scaling activities before the effects of previous activities are visible.

With a target tracking scaling policy, you can increase or decrease the current capacity of the group based on a target value for a specific metric. This policy will help resolve the over-provisioning of your resources. The scaling policy adds or removes capacity as required to keep the metric at, or close to, the specified target value. In addition to keeping the metric close to the target value, a target tracking scaling policy also adjusts to changes in the metric due to a changing load pattern.

Hence, the correct answer is: Use target tracking scaling.

The option that says: Use simple scaling is incorrect because you need to wait for the cooldown period to complete before initiating additional scaling activities. Target tracking or step scaling policies can trigger a scaling activity immediately without waiting for the cooldown period to expire.

The option that says: Use scheduled scaling is incorrect because this policy is mainly used for predictable traffic patterns. You need to use the target tracking scaling policy to optimize the cost of your infrastructure without affecting the performance.

The option that says: Use suspend and resume scaling is incorrect because this type is used to temporarily pause scaling activities triggered by your scaling policies and scheduled actions.

 

References:

https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scaling-target-tracking.html

https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html

 

Check out this AWS Auto Scaling Cheat Sheet:

https://tutorialsdojo.com/aws-auto-scaling/



15. Question
A Solutions Architect is working for a large global media company with multiple office locations all around the world. The Architect is instructed to build a system to distribute training videos to all employees.

Using Amazon CloudFront, what method would be used to serve content that is stored in Amazon S3 but not publicly accessible from S3 directly?

Create a web ACL in AWS WAF to block any public S3 access and attach it to the CloudFront distribution.
Create an Origin Access Control (OAC) for CloudFront and grant access to the objects in your S3 bucket to that OAC.
Create an Identity and Access Management (IAM) user for CloudFront and grant access to the objects in your S3 bucket to that IAM user.
Create an S3 bucket policy that lists the CloudFront distribution ID as the principal and the target bucket as the Amazon Resource Name (ARN).
Incorrect
When you create or update a distribution in CloudFront, you can add an origin access Control (OAC) and automatically update the bucket policy to give the origin access control permission to access your bucket. Alternatively, you can choose to manually change the bucket policy or change ACLs, which control permissions on individual objects in your bucket.

Amazon CloudFront Origin Access Control

You can update the Amazon S3 bucket policy using either the AWS Management Console or the Amazon S3 API:

– Grant the CloudFront origin access control the applicable permissions on the bucket.

– Deny access to anyone that you don’t want to have access using Amazon S3 URLs.

Hence, the correct answer is: Create an Origin Access Control (OAC) for CloudFront and grant access to the objects in your S3 bucket to that OAC.

The option that says: Create an Identity and Access Management (IAM) user for CloudFront and grant access to the objects in your S3 bucket to that IAM user is incorrect because you cannot directly create an IAM User for a specific Amazon CloudFront distribution. You have to use an origin access control (OAC) instead.

The option that says: Create an S3 bucket policy that lists the CloudFront distribution ID as the principal and the target bucket as the Amazon Resource Name (ARN) is incorrect. While you can typically specify AWS accounts, IAM users, and IAM roles as principals in an S3 bucket policy, you cannot directly use a CloudFront distribution ID as a principal in an S3 bucket policy. Instead, you must define the CloudFront service as the Principal and restrict access to your CF distribution using the Condition policy. Therefore, this is not the correct method for the given scenario.

The option that says: Create a web ACL in AWS WAF to block any public S3 access and attach it to the CloudFront distribution is incorrect because AWS WAF is primarily used to protect your applications from common web vulnerabilities and not to ensure exclusive access to CloudFront.

 

References:

https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html

https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/SecurityAndPrivateContent.html

 

Check out this Amazon CloudFront Cheat Sheet:

https://tutorialsdojo.com/amazon-cloudfront/

 

Comparison of AWS Services Cheat Sheets:

https://tutorialsdojo.com/comparison-of-aws-services/
