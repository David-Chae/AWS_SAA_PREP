Design Secure Architectures
12 of 15 correct

Question 3
A company is designing an AWS solution to store sensitive customer records in Amazon S3. The architecture must enforce role-based access, automatically transition infrequently accessed data to a lower-cost storage class, and ensure encryption at rest. Operational overhead must be kept to a minimum. Which solution best meets these requirements?

Correct Answers
Selected
Attach IAM policies to user roles, enable S3 Lifecycle rules for storage transition, and use SSE-S3 for encryption.

Rationale: Attaching IAM policies to user roles allows precise control over who can access S3 resources based on their assigned roles. S3 Lifecycle rules automate the transition of objects to lower-cost storage classes, reducing manual intervention. SSE-S3 provides server-side encryption managed by AWS, simplifying encryption management and ensuring data is encrypted at rest.

Incorrect Answers
Use S3 bucket policies for access control, transition data manually to Glacier, and encrypt with customer-managed KMS keys.

Rationale: S3 bucket policies can control access but may be less granular than IAM role-based policies for enforcing role-based access. Manually transitioning data to Glacier requires ongoing operational effort. Customer-managed KMS keys provide strong encryption but add complexity due to key management responsibilities.

Set object-level permissions in the S3 console, use S3 Intelligent-Tiering manually, and enable default encryption with SSE-KMS.

Rationale: Managing permissions at the object level can become complex and difficult to maintain at scale. While S3 Intelligent-Tiering automates cost optimization, manually managing it contradicts the goal of minimizing operational overhead. SSE-KMS offers advanced encryption features but requires additional management compared to AWS-managed keys.

Enable S3 Object Lock for compliance, attach SCPs (Service Control Policies) for access control, and configure client-side encryption.

Rationale: S3 Object Lock is designed for data immutability and compliance purposes, which may not be necessary for this use case. SCPs are used to enforce policies at the AWS organization level rather than direct resource access control. Client-side encryption increases operational complexity as encryption and key management responsibilities shift to the client side.


Question 7
You are a Solutions Architect supporting a media company launching a trailer website for a major movie. The site is hosted behind an Application Load Balancer (ALB) and fronted by Amazon CloudFront. A previous release suffered a significant DDoS attack that disrupted service for two days. The security team asks you to help strengthen the architecture to better handle such incidents. The solution should improve mitigation, provide support during events, and reduce the risk of unexpected cost increases due to malicious traffic.

Which approach should you recommend to meet these requirements?

Correct Answers
Selected
Enable AWS Shield Advanced and associate protection with the CloudFront distribution and ALB.

Rationale: Shield Advanced offers enhanced DDoS protection (Layers 3, 4, 7), 24/7 Shield Response Team support, and cost protection against scaling charges during attacks. It integrates with CloudFront and ALB.

Incorrect Answers
Apply rate-based rules and IP filtering using AWS WAF on both CloudFront and the ALB.

Rationale: AWS WAF can mitigate some Layer 7 attacks via rate limiting and IP filtering. However, WAF alone does not provide cost protection or 24/7 support during large DDoS attacks.

Configure CloudFront with AWS Shield Standard and monitor access logs to detect anomalies.

Rationale: AWS Shield Standard is automatically enabled and protects against common Layer 3 and 4 attacks but does not offer advanced mitigation, cost protection, or 24/7 support. Monitoring logs is reactive and insufficient for proactive mitigation.

Use Amazon GuardDuty to detect potential threats and automate responses with Lambda.

Rationale: Amazon GuardDuty detects suspicious activity but does not mitigate DDoS attacks or provide cost protection. It is a threat detection service, not a DDoS mitigation or cost control solution.



Question 13
You have a multi-tier web application running on Amazon EC2 instances in a VPC. The web tier must allow HTTP traffic from the internet, and the application tier should accept traffic only from the web tier. You want secure, keyless access to all instances without opening inbound SSH ports. Which actions should you take?

Correct Answers
Selected
Allow inbound HTTP (port 80) from anywhere 0.0.0.0/0 to the web tier.

Rationale: This action allows public HTTP access to the web tier as required.

Selected
Configure the application tier’s security group to allow inbound traffic only from the web tier’s security group.

Rationale: This action restricts application tier inbound traffic to only instances in the web tier by referencing the web tier security group, enforcing least privilege.

Selected
Use AWS Systems Manager Session Manager for keyless, secure access to all instances without opening SSH ports.

Rationale: This action provides secure, keyless access without opening SSH ports, reducing attack surface and operational overhead.

Incorrect Answers
Allow inbound HTTP (port 80) from your office IP to the web tier.

Rationale: This action restricts web tier HTTP to office IP only, limiting legitimate user access.

Enable SSH access with key pairs on all instances and open inbound port 22.

Rationale: This action requires managing SSH keys and opening inbound SSH ports, increasing security risk.

Configure the application tier’s security group to allow inbound traffic from the internet on a custom application port.

Rationale: Application tier should not accept internet traffic; this increases exposure and violates least privilege.


Question 14
A company is expanding its AWS environment by creating multiple accounts for different teams and projects. The central IT team needs to ensure workloads are separated, enforce consistent security policies across accounts, and simplify cost management through centralized billing. Which AWS features should the company implement to meet these requirements?

Correct Answers
Selected
Group accounts into Organizational Units (OUs) using AWS Organizations.

Rationale: Organizing accounts into OUs allows grouping by function and applying policies consistently across related accounts.

Selected
Use Service Control Policies (SCPs) in AWS Organizations to enforce permission boundaries across accounts.

Rationale: SCPs provide centralized permission boundaries that apply to all users and roles in accounts, enforcing security policies.

Selected
Enable consolidated billing to centralize cost management.

Rationale: Consolidated billing aggregates costs from multiple accounts into a single bill, simplifying cost management and providing visibility.

Incorrect Answers
Use AWS IAM roles exclusively to manage access across multiple accounts without grouping or centralized policy enforcement.

Rationale: IAM roles manage permissions but do not provide account grouping or centralized policy enforcement, limiting governance capabilities.

Deploy AWS Control Tower to automate account provisioning and enforce guardrails.

Rationale: AWS Control Tower automates account provisioning and governance but is optional; it is not required to meet the core requirements stated.

Use AWS Systems Manager to automate operational tasks.

Rationale: AWS Systems Manager automates operational tasks but does not manage accounts or billing, so it does not address the scenario’s core needs.



Question 15
A company uses Amazon RDS for PostgreSQL to store critical data. Compliance requires that database backups be retained for seven years and replicated to a different AWS Region to protect against regional failures. Which solution meets these requirements with minimal operational overhead?

Correct Answers
Enable automated backups in Amazon RDS and use AWS Backup to create and copy snapshots to a different Region.

Rationale: AWS Backup integrates with Amazon RDS to automate snapshot creation, cross-Region replication, and long-term retention policies. This meets the 7-year retention and cross-Region replication compliance requirements with minimal operational overhead.

Incorrect Answers
Create cross-Region read replicas and manually retain transaction logs for seven years.

Rationale: Cross-Region read replicas provide data redundancy but are not backups and do not satisfy long-term retention requirements. Manually retaining transaction logs for seven years is operationally complex and error prone.

Schedule RDS snapshots with AWS Systems Manager and store them in Amazon S3 Glacier for long-term retention.

Rationale: Scheduling snapshots via Systems Manager and storing them in S3 Glacier is possible but requires manual management and additional operational effort. Native RDS snapshots are not directly stored in Glacier without export or copy.

Selected
Enable multi-AZ deployment and export snapshots to Amazon S3 in a different Region.

Rationale: Multi-AZ deployment provides high availability within a single Region only. Exporting snapshots to S3 does not automatically replicate them to another Region or ensure long-term retention.



Question 16
You manage a large fleet of EC2 instances. After a recent security breach, your manager asks you to identify an AWS service that can install an agent on your EC2 instances, perform security assessments against hardened benchmarks, and report findings and violations. Which service should you use?

Correct Answers
Selected
Amazon Inspector

Rationale: Amazon Inspector installs an agent on EC2 instances (or uses agentless scanning), performs vulnerability and configuration assessments using security benchmarks such as the Center for Internet Security (CIS) benchmark, and generates detailed findings with prioritized severity levels. It directly supports agent-based assessments and reporting.

Incorrect Answers
Amazon GuardDuty

Rationale: GuardDuty is a threat detection service that analyzes AWS CloudTrail, VPC Flow Logs, and DNS logs to identify suspicious activity. It does not install agents on EC2 instances nor perform vulnerability assessments against hardened templates.

AWS Security Hub

Rationale: Security Hub aggregates and prioritizes security findings from multiple AWS services including Inspector and GuardDuty, providing a centralized view. However, it does not perform assessments or install agents itself.

AWS Trusted Advisor

Rationale: Trusted Advisor offers best practice checks across AWS services, including security, but it does not install agents or perform detailed vulnerability assessments on EC2 instances. It provides high-level recommendations rather than in-depth scanning.



Question 20
Under the AWS Shared Responsibility Model, which tasks is the customer responsible for?

Correct Answers
Selected
Configuring security group rules to control traffic to EC2 instances

Rationale: Customers are responsible for configuring security group rules to control traffic to EC2 instances (security in the cloud).

Selected
Encrypting sensitive data stored in Amazon S3

Rationale: Even though server-side encryption with Amazon S3 managed keys (SSE-S3) is enabled by default for all new objects (since Jan 5, 2023), customers remain responsible for protecting their data—choosing encryption approaches (for example, Server-Side Encryption with AWS Key Management Service (SSE-KMS) with customer managed keys), enforcing policies, and managing access controls. Default encryption does not remove customer responsibility for data protection.

Incorrect Answers
Managing physical access to servers in AWS data centers

Rationale: Physical access to AWS data centers is AWS’s responsibility (security of the cloud).

Patching the underlying hypervisor used by AWS services

Rationale: AWS patches the underlying hypervisor and infrastructure components.

Managing the redundancy of AWS networking infrastructure

Rationale: AWS manages redundancy of networking infrastructure as part of the cloud infrastructure.


Question 25
A media production company needs a dedicated and secure connection between its on-premises data center and AWS. The company wants to transfer large video files to a VPC while minimizing latency and avoiding the use of the public internet. Which solution best meets these requirements?

Correct Answers
Selected
Configure a private virtual interface (VIF) over AWS Direct Connect to connect to the VPC.

Rationale: AWS Direct Connect with a private virtual interface provides a dedicated, secure, low-latency connection directly to the company’s VPC, avoiding the public internet.

Incorrect Answers
Establish a Site-to-Site VPN and use AWS Transit Gateway to route traffic to the VPC.

Rationale: Site-to-Site VPN uses the public internet, which contradicts the requirement to avoid public internet usage and minimize latency.

Create a public virtual interface (VIF) over AWS Direct Connect to access the VPC.

Rationale: AWS Direct Connect with a public virtual interface connects to public AWS services such as Amazon S3. It does not connect directly to a VPC and therefore does not provide a dedicated connection to the VPC.

Use AWS Transit Gateway and VPC peering to connect the on-premises network.

Rationale: Transit Gateway and VPC peering are AWS internal networking features; they do not establish dedicated connections between on-premises data centers and AWS.



Question 29
You are a Solutions Architect for a healthcare company subject to strict compliance requirements. You are designing access policies for AWS Key Management Service (AWS KMS) to manage encryption keys used by various teams. Which actions help ensure secure and appropriate use of the encryption keys?

Correct Answers
Selected
Define key policies that grant least-privilege access to IAM roles based on each team’s operational needs.

Rationale: Defining least-privilege key policies tailored to each team’s needs ensures secure, appropriate access and meets compliance requirements. Key policies are the primary access control mechanism in AWS KMS.

Create customer managed keys (CMKs) with key policies that restrict administrative access to a limited set of roles.

Rationale: Restricting administrative access to a limited set of roles via CMK key policies is essential for secure key management and compliance.

Incorrect Answers
Use key policies that grant full administrative access to all IAM users in the account to avoid operational delays.

Rationale: Granting full administrative access to all IAM users violates the principle of least privilege and increases security risks. This is not compliant with AWS KMS best practices.

Rely solely on IAM policies to manage access to KMS keys and leave the key policy empty.

Rationale: Leaving the key policy empty and relying solely on IAM policies is insecure because a key policy must explicitly grant access; without it, no principal has permission to use the key.

Selected
Enable key rotation to ensure that keys are replaced automatically without requiring changes to access policies.

Rationale: While key rotation is a security best practice for key lifecycle management, it does not affect access permissions or policies and thus does not fulfill the core requirement of access control.




Question 30
You are designing a secure application that needs to retrieve database credentials at runtime. The security team requires that the credentials are never hardcoded, must be rotated automatically without redeploying the application, and must be securely accessible from workloads running in other AWS accounts. Which approach using native AWS services best meets these requirements?

Correct Answers
Selected
Use AWS Secrets Manager with cross-account access configured through resource-based policies.

Rationale: AWS Secrets Manager supports automatic secret rotation, secure storage, and retrieval. It supports cross-account access via resource-based policies and customer-managed KMS keys, fulfilling all requirements.

Incorrect Answers
Store credentials in an encrypted S3 object and access them using presigned URLs.

Rationale: Storing secrets in S3 is not a best practice for secret management. It lacks automatic rotation and fine-grained access control. Presigned URLs do not provide secure, auditable secret retrieval and do not support cross-account secure access natively.

Use AWS Systems Manager Parameter Store in SecureString mode with rotation scripts.

Rationale: Parameter Store supports SecureString and can be used with rotation scripts, but it does not natively support automatic rotation like Secrets Manager. Cross-account access is more complex and less straightforward than Secrets Manager.

Store credentials as environment variables in Lambda and encrypt them with KMS.

Rationale: Environment variables are static and require redeployment to update. They do not support automatic rotation without redeployment and do not provide cross-account secure access.



Question 39
A developer reports that their application fails with an AccessDeniedException when encrypting data using a customer-managed AWS KMS key in the same AWS account. The application runs on an Amazon EC2 instance with an attached IAM role. What is the most likely cause?

Correct Answers
Selected
The IAM role does not have permission to use the KMS key in its identity policy.

Rationale: The IAM role must have explicit permissions to use the KMS key. Missing or insufficient permissions cause AccessDeniedException errors. Both the IAM role's identity policy and the KMS key’s key policy must permit access.

Incorrect Answers
The EC2 instance does not have internet access to reach the KMS service endpoint.

Rationale: Lack of internet access causes network errors, not AccessDeniedException. KMS is a regional service and can be accessed over private endpoints (VPC interface endpoints). Internet access is not required if the appropriate endpoint exists or KMS is reachable via VPC routing.

The KMS key is pending deletion and cannot be used until it is restored.

Rationale: A pending deletion key cannot be used. If a key is pending deletion, KMS will return a different error: KMSInvalidStateException, not AccessDeniedException.

The EC2 instance is using a service-linked role that cannot access customer-managed keys.

Rationale: Service-linked roles are for AWS services, not for EC2 instances launched by users. This is unlikely to cause the error.



Question 42
You are designing a solution to implement AWS GuardDuty across multiple AWS accounts in your organization. Your goals are to centralize threat detection and minimize management overhead. Which actions should you include in your design to meet these goals?

Correct Answers
Designate a single AWS account as the GuardDuty administrator account to manage findings for all member accounts.

Rationale: Designating one AWS account as the GuardDuty administrator centralizes threat detection and management across all member accounts. This approach reduces complexity and consolidates findings for easier analysis.

Selected
Use AWS Organizations integration to automatically enable GuardDuty across all existing and new accounts.

Rationale: Integrating GuardDuty with AWS Organizations allows automatic enabling of GuardDuty on all existing and future accounts. This automation minimizes manual effort and ensures consistent security coverage as your organization grows.

Incorrect Answers
Enable GuardDuty in each member account and configure each account independently.

Rationale: Enabling GuardDuty independently in each member account increases management overhead and risks inconsistent configurations. Centralizing management simplifies monitoring and response.

Selected
Configure Amazon CloudWatch Events to forward GuardDuty findings to a centralized Security Information and Event Management (SIEM) system for analysis.

Rationale: Forwarding GuardDuty findings to a centralized SIEM via CloudWatch Events is a useful practice for extended analysis but does not inherently centralize GuardDuty management or reduce operational overhead. It is an optional integration step beyond the core design requirements.




Create a VPC gateway endpoint for Amazon SQS and configure a NAT gateway for AWS Systems Manager.

Rationale: Gateway endpoints only support Amazon S3 and DynamoDB. Using a NAT gateway exposes traffic to the internet and increases operational overhead.

Create gateway endpoints for Amazon SQS and Systems Manager and update route tables.

Rationale: Gateway endpoints only support Amazon S3 and DynamoDB, so this option is invalid.

Use an AWS Transit Gateway to route traffic to Amazon SQS and AWS Systems Manager.

Rationale: AWS Transit Gateway connects VPCs and on-premises networks but does not provide direct connectivity to AWS services such as SQS or Systems Manager.



Question 51
You are configuring two EC2 instances within the same VPC and Availability Zone, but in different subnets. The first instance will host the main company website, and the second instance will host the database. To ensure the website can communicate securely and reliably with the database, what steps should you take?

Correct Answers
Selected
Ensure Network ACLs allow inbound and outbound traffic between the two subnets.

Rationale: NACLs act as stateless firewalls at the subnet level, controlling inbound and outbound traffic. By allowing only necessary traffic between subnets, they add an extra layer of security and help prevent disruptions, ensuring reliable communication. Properly configured NACLs are essential because they can block traffic even if security groups allow it.

Selected
Configure security groups to allow communication on the required ports and protocols.

Rationale: Security groups are stateful firewalls attached to instances. They control inbound and outbound traffic at the instance level. Properly configuring security groups to allow traffic on the required ports (e.g., HTTP/HTTPS for the website, database port like 3306 for MySQL) ensures secure and controlled communication between the two instances.

Incorrect Answers
Assign an Elastic IP address to each instance for communication.

Rationale: Elastic IPs provide public IP addresses for instances, primarily used for internet-facing resources. For communication within the same VPC and Availability Zone, instances use private IP addresses. Assigning Elastic IPs is unnecessary and does not affect internal communication.

Place both instances in the same placement group for better performance.

Rationale: Placement groups influence the physical placement of instances to optimize for low latency or high throughput. They do not impact network communication permissions or routing between subnets. This step is irrelevant to enabling communication between instances in different subnets.

Set up a Virtual Private Gateway (VGW) to enable communication between the instances.

Rationale: A VGW is used to connect a VPC to external networks such as on-premises data centers via VPN or AWS Direct Connect. It is not required for communication between instances within the same VPC, even if they are in different subnets.



Question 53
A news media company hosts hundreds of photos of television personalities in an Amazon S3 bucket. These photos are accessed nationwide by the company’s local affiliates through a web application. Recently, unauthorized external websites have been pirating the photos. What is the best way to securely distribute the photos to authorized affiliates while minimizing operational overhead and allowing users to access multiple photos during a session?

Correct Answers
Selected
Disable public access on the S3 bucket and use Amazon CloudFront with signed cookies to distribute the photos securely.

Rationale: This is the best practice for securely delivering multiple files during a user session. Disabling public access on S3 prevents direct access, while CloudFront provides secure, cached distribution. Signed cookies allow authorized users to access multiple photos without needing individual signed URLs, minimizing operational overhead. Though it requires some setup, this approach balances strong security, scalability, and efficient access for affiliates.

Incorrect Answers
Disable public access on the S3 bucket and provide authorized users with pre-signed URLs for each photo.

Rationale: Pre-signed URLs offer secure, temporary access to individual S3 objects and are effective for short-term or single-object access. However, they require generating and managing a unique URL for each photo and user, creating significant operational overhead. This method also lacks CDN caching, leading to higher latency and cost when serving a large number of users nationwide.

Enable public access and use Amazon CloudFront with signed URLs to distribute the photos securely.

Rationale: While CloudFront with signed URLs can securely restrict access at the CDN layer, enabling public access on the S3 bucket exposes the content to direct access and piracy, defeating the purpose of security. Even if public access were disabled, signed URLs are still less efficient than signed cookies for users accessing multiple photos in a session, due to the need to generate a URL for each object.

Store the photos in an Amazon RDS database and require users to register and log in.

Rationale: While user authentication is important, storing static content like photos in a relational database is inefficient, expensive, and adds unnecessary complexity. RDS is not optimized for serving large volumes of static files, resulting in higher latency and operational overhead. S3 and CloudFront are far better suited for secure, scalable static content delivery.
