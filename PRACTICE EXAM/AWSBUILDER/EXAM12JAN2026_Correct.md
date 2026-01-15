이 질문이 **진짜 중요한 분기점**이야.
지금 네 상태를 정확히 말하면:

> **“문제를 맞히긴 했지만, 머릿속에서 ‘왜 이게 정답인지’가 자동으로 재생되지 않는 상태”**

이 상태를 그대로 두고 가면 **실전에서 반드시 다시 흔들린다**.
반대로, 지금 이걸 정리하면 **운이 개입될 여지가 거의 없는 합격 상태**로 올라간다.

아래는 **‘맞았지만 운이 섞인 문제’를 100% 실력으로 바꾸는 방법**이야.

---

## 1️⃣ 지금 네가 ‘운으로 맞췄다’고 느끼는 이유 (정확한 진단)

네가 맞힌 문제들  을 보면 공통점이 있다:

### ⚠️ 특징

* 정답은 골랐지만
* ❌ **다른 선택지가 왜 틀렸는지 즉시 설명하기 어렵다**
* ❌ 서비스 이름이 바뀌면 다시 헷갈릴 가능성 높음
* ❌ “이 문제 다시 나오면 또 맞출까?”가 불확실

👉 이건 **개념 암기 상태**고
👉 시험에서는 **판단 자동화 상태**가 필요해.

---

## 2️⃣ “운으로 맞은 문제”를 실력으로 바꾸는 핵심 공식

### ✅ 공식 하나만 기억해

> **정답을 외우지 말고, 오답을 ‘즉시 제거하는 이유’를 외워라**

시험은:

* 정답을 찾는 게임 ❌
* **틀린 선택지를 얼마나 빨리 제거하느냐의 게임** ⭕

---

## 3️⃣ 네가 맞힌 문제들을 “판단 규칙”으로 바꿔보자

아래는 네가 맞힌 문제들을 **시험용 판단 문장**으로 변환한 거야.

---

### 🔹 DynamoDB + VPC 문제

**문제 핵심**

* Public service
* Public Internet 통과 금지
* Cross-account backup 필요

**시험 판단 규칙**

> “DynamoDB + VPC + 인터넷 미경유 = Gateway Endpoint”

> “DynamoDB cross-account backup = AWS Backup (PITR 아님)”

👉 이 두 문장이 동시에 떠오르면 **다른 선택지는 볼 필요도 없음** 

---

### 🔹 IPv6 아웃바운드만 허용 문제

**판단 규칙**

> “IPv6 outbound only + inbound 차단 = Egress-Only IGW”

> “Traffic inspection/filtering = AWS Network Firewall”

👉 NAT, IGW, GuardDuty, Traffic Mirroring은 **역할 불일치로 즉시 제거** 

---

### 🔹 Aurora 읽기 병목 문제

**판단 규칙**

> “읽기 트래픽 증가 + 비용 민감 = Aurora Auto Scaling”

👉 Global DB / Cross-region은
👉 **‘글로벌’이라는 단어가 없으면 90% 미끼** 

---

### 🔹 S3 Standard-IA 문제

**판단 규칙**

> “덜 자주 접근 + 즉시 접근 = Standard-IA”

> “자동 이동 = Intelligent-Tiering (절대 IA 아님)”

👉 Glacier / Archive 보이면 즉시 제거 

---

### 🔹 Kinesis 데이터 유실 문제

**판단 규칙**

> “Kinesis 기본 설정 = 24시간 보존”

👉 S3 데이터 손실, 권한 문제는 **확률적으로 AWS 시험에서 거의 안 나오는 선택지** 

---

### 🔹 Lambda + VPC + 오류 문제

**판단 규칙**

> “Lambda VPC 오류 + 특정 시간대 = ENI/IP 고갈”

👉 IAM, SG, NAT 문제는
👉 **항상 ‘전체 실패’ 시나리오에서만 정답** 

---

### 🔹 Hybrid 연결 문제

**판단 규칙**

> “고대역폭 + 일관된 연결 = Direct Connect”

👉 VPN / Transit / TGW는
👉 **‘연결 방식’이지 ‘물리적 전용선’이 아님** 

---

## 4️⃣ 실전에서 “절대 흔들리지 않게 만드는 훈련법”

### 📌 Step 1. 맞힌 문제를 다시 푼다 (중요)

* 답 가리고
* **오답부터 제거**
* 제거 이유를 말로 설명

👉 1초라도 머뭇거리면 **그 문제는 아직 운이다**

---

### 📌 Step 2. 각 문제당 “판단 문장 1~2개”만 남긴다

예:

* “IPv6 outbound only = Egress-only IGW”
* “비용 최적 + 자동 = Target Tracking / Auto Scaling”

👉 이 문장들이 시험장에서 자동으로 떠오르면 합격

---

### 📌 Step 3. 서비스 역할 충돌 감지 훈련

시험에서는 자주 이런 미끼가 나온다:

* GuardDuty로 트래픽 차단 ❌
* Firewall Manager로 inspection ❌
* IAM User로 CloudFront 접근 ❌

👉 **“이 서비스 원래 그거 하는 애야?”**
👉 이 질문이 자동으로 나오면 흔들리지 않는다

---

## 5️⃣ 지금 네 상태 요약 (중요)

* ❌ 운으로 붙는 단계 아님
* ❌ 다시 처음부터 공부할 필요 없음
* ✅ **판단 규칙만 정리하면 안정 합격권**
* ✅ 실전에서 틀릴 문제 수가 급감하는 단계

---

3. Question
A GraphQL API hosted is hosted in an Amazon EKS cluster with AWS Fargate launch type and deployed using AWS SAM. The API is connected to an Amazon DynamoDB table with DynamoDB Accelerator (DAX) as its data store. Both resources are hosted in the us-east-1 region.

The AWS IAM authenticator for Kubernetes is integrated into the EKS cluster for role-based access control (RBAC) and cluster authentication. A solutions architect must improve network security by preventing database calls from traversing the public internet. An automated cross-account backup for the DynamoDB table is also required for long-term retention.

Which of the following should the solutions architect implement to meet the requirement?

Create a DynamoDB gateway endpoint. Associate the endpoint to the appropriate route table. Use AWS Backup to automatically copy the on-demand DynamoDB backups to another AWS account for disaster recovery.

Create a DynamoDB interface endpoint. Set up a stateless rule using AWS Network Firewall to control all outbound traffic to only use the dynamodb.us-east-1.amazonaws.com endpoint. Integrate the DynamoDB table with Amazon Timestream to allow point-in-time recovery from a different AWS account.

Create a DynamoDB gateway endpoint. Set up a Network Access Control List (NACL) rule that allows outbound traffic to the dynamodb.us-east-1.amazonaws.com gateway endpoint. Use the built-in on-demand DynamoDB backups for cross-account backup and recovery.
Create a DynamoDB interface endpoint. Associate the endpoint to the appropriate route table. Enable Point-in-Time Recovery (PITR) to restore the DynamoDB table to a particular point in time on the same or a different AWS account.
Correct
Since DynamoDB tables are public resources, applications within a VPC rely on an Internet Gateway to route traffic to/from Amazon DynamoDB. You can use a Gateway endpoint if you want to keep the traffic between your VPC and Amazon DynamoDB within the Amazon network. This way, resources residing in your VPC can use their private IP addresses to access DynamoDB with no exposure to the public internet.

When you create a DynamoDB Gateway endpoint, you specify the VPC where it will be deployed as well as the route table that will be associated with the endpoint. The route table will be updated with an Amazon DynamoDB prefix list (list of CIDR blocks) as the destination and the endpoint’s ID as the target.

amazon dynamodb gateway endpoint

DynamoDB on-demand backups are available at no additional cost beyond the normal pricing that’s associated with backup storage size. DynamoDB on-demand backups cannot be copied to a different account or Region. To create backup copies across AWS accounts and Regions and for other advanced features, you should use AWS Backup.

With AWS Backup, you can configure backup policies and monitor activity for your AWS resources and on-premises workloads in one place. Using DynamoDB with AWS Backup, you can copy your on-demand backups across AWS accounts and Regions, add cost allocation tags to on-demand backups, and transition on-demand backups to cold storage for lower costs. To use these advanced features, you must opt into AWS Backup. Opt-in choices apply to the specific account and AWS Region, so you might have to opt into multiple Regions using the same account.

Hence, the correct answer is: Create a DynamoDB gateway endpoint. Associate the endpoint to the appropriate route table. Use AWS Backup to automatically copy the on-demand DynamoDB backups to another AWS account for disaster recovery.

The option that says: Create a DynamoDB interface endpoint. Associate the endpoint to the appropriate route table. Enable Point-in-Time Recovery (PITR) to restore the DynamoDB table to a particular point in time on the same or a different AWS account is incorrect. While this option addresses the network security requirement, Point-in-Time Recovery (PITR) is only used for restoring a DynamoDB table to a specific point in time within the same AWS account and region. It does not support cross-account backups or long-term retention. If this functionality is needed, you have to use the AWS Backup service instead.

The option that says: Create a DynamoDB gateway endpoint. Set up a Network Access Control List (NACL) rule that allows outbound traffic to the dynamodb.us-east-1.amazonaws.com gateway endpoint. Use the built-in on-demand DynamoDB backups for cross-account backup and recovery is incorrect because using a Network Access Control List alone is not enough to prevent traffic traversing to the public Internet. Moreover, you cannot copy DynamoDB on-demand backups to a different account or Region.

The option that says: Create a DynamoDB interface endpoint. Set up a stateless rule using AWS Network Firewall to control all outbound traffic to only use the dynamodb.us-east-1.amazonaws.com endpoint. Integrate the DynamoDB table with Amazon Timestream to allow point-in-time recovery from a different AWS account is incorrect. Keep in mind that the dynamodb.us-east-1.amazonaws.com is a public service endpoint for Amazon DynamoDB. Since the application is able to communicate with Amazon DynamoDB prior to the required architectural change, it’s implied that no firewalls (security group, NACL, etc.) are blocking traffic to/from Amazon DynamoDB, hence, adding an NACL rule to allow outbound traffic to DynamoDB is unnecessary. Furthermore, the use of the AWS Network Firewall in this solution is simply incorrect as you have to integrate this with your Amazon VPC. The use of Amazon Timestream is also wrong since this is a time series database service in AWS for IoT and operational applications. You cannot directly integrate DynamoDB and Amazon Timestream for the purpose of point-in-time data recovery.

 

References:

https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/vpc-endpoints-dynamodb.html

https://aws.amazon.com/blogs/database/how-to-configure-a-private-network-environment-for-amazon-dynamodb-using-vpc-endpoints/

https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/BackupRestore.html

 

Check out this Amazon DynamoDB Cheat sheet:

https://tutorialsdojo.com/amazon-dynamodb


6. Question
A payment processing company plans to migrate its on-premises application to an Amazon EC2 instance. An IPv6 CIDR block is attached to the company’s Amazon VPC. Strict security policy mandates that the production VPC must only allow outbound communication over IPv6 between the instance and the internet but should prevent the internet from initiating an inbound IPv6 connection. The new architecture should also allow traffic flow inspection and traffic filtering.

What should a solutions architect do to meet these requirements?

Launch the EC2 instance to a private subnet and attach AWS PrivateLink interface endpoint to the VPC to control outbound IPv6 communication to the internet. Use Amazon GuardDuty to set up the required rules for traffic inspection and traffic filtering.
Launch the EC2 instance to a private subnet and attach an Egress-Only Internet Gateway to the VPC to allow outbound IPv6 communication to the internet. Use AWS Network Firewall to set up the required rules for traffic inspection and traffic filtering.
Launch the EC2 instance to a public subnet and attach an Internet Gateway to the VPC to allow outbound IPv6 communication to the internet. Use Traffic Mirroring to set up the required rules for traffic inspection and traffic filtering.
Launch the EC2 instance to a private subnet and attach a NAT Gateway to the VPC to allow outbound IPv6 communication to the internet. Use AWS Firewall Manager to set up the required rules for traffic inspection and traffic filtering.
Correct
An egress-only internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows outbound communication over IPv6 from instances in your VPC to the internet and prevents it from initiating an IPv6 connection with your instances.

Egress Only Internet Gateway

IPv6 addresses are globally unique and are therefore public by default. If you want your instance to be able to access the internet, but you want to prevent resources on the internet from initiating communication with your instance, you can use an egress-only internet gateway.

A subnet is a range of IP addresses in your VPC. You can launch AWS resources into a specified subnet. Use a public subnet for resources that must be connected to the internet and a private subnet for resources that won’t be connected to the internet.

AWS Network Firewall is a managed service that makes it easy to deploy essential network protections for all of your Amazon Virtual Private Clouds (VPCs). The service can be set up with just a few clicks and scales automatically with your network traffic, so you don’t have to worry about deploying and managing any infrastructure. AWS Network Firewall includes features that provide protection from common network threats.

AWS Network Firewall Filter & Inspection

AWS Network Firewall’s stateful firewall can incorporate context from traffic flows, like tracking connections and protocol identification, to enforce policies such as preventing your VPCs from accessing domains using an unauthorized protocol. AWS Network Firewall’s intrusion prevention system (IPS) provides active traffic flow inspection so you can identify and block vulnerability exploits using signature-based detection. AWS Network Firewall also offers web filtering that can stop traffic to known bad URLs and monitor fully qualified domain names.

In this scenario, you can use an egress-only internet gateway to allow outbound IPv6 communication to the internet and then use the AWS Network Firewall to set up the required rules for traffic inspection and traffic filtering.

Hence, the correct answer is: Launch the EC2 instance to a private subnet and attach an Egress-Only Internet Gateway to the VPC to allow outbound IPv6 communication to the internet. Use AWS Network Firewall to set up the required rules for traffic inspection and traffic filtering.

The option that says: Launch the EC2 instance to a private subnet and attach AWS PrivateLink interface endpoint to the VPC to control outbound IPv6 communication to the internet. Use Amazon GuardDuty to set up the required rules for traffic inspection and traffic filtering is incorrect because the AWS PrivateLink (which is also known as VPC Endpoint) is just a highly available, scalable technology that enables you to privately connect your VPC to the AWS services as if they were in your VPC. This service is not capable of controlling outbound IPv6 communication to the Internet. Furthermore, the Amazon GuardDuty service doesn’t have the features to do traffic inspection or filtering.

The option that says: Launch the EC2 instance to a public subnet and attach an Internet Gateway to the VPC to allow outbound IPv6 communication to the internet. Use Traffic Mirroring to set up the required rules for traffic inspection and traffic filtering is incorrect because an Internet Gateway does not limit or control any outgoing IPv6 connection. Take note that the requirement is to prevent the Internet from initiating an inbound IPv6 connection to your instance. This solution allows all kinds of traffic to initiate a connection to your EC2 instance hence, this option is wrong. In addition, the use of Traffic Mirroring is not appropriate as well. This is just an Amazon VPC feature that you can use to copy network traffic from an elastic network interface of type interface, not to filter or inspect the incoming/outgoing traffic.

The option that says: Launch the EC2 instance to a private subnet and attach a NAT Gateway to the VPC to allow outbound IPv6 communication to the internet. Use AWS Firewall Manager to set up the required rules for traffic inspection and traffic filtering is incorrect. While NAT Gateway has a NAT64 feature that translates an IPv6 address to IPv4, it will not prevent inbound IPv6 traffic from reaching the EC2 instance. You have to use the egress-only Internet Gateway instead. Moreover, the AWS Firewall Manager is neither capable of doing traffic inspection nor traffic filtering.

 

References:

https://docs.aws.amazon.com/vpc/latest/userguide/egress-only-internet-gateway.html

https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html

https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html

 

Check out this Amazon VPC Cheat Sheet:

https://tutorialsdojo.com/amazon-vpc/


8. Question
An e-commerce company runs a highly scalable web application that depends on an Amazon Aurora database. As the number of users increases, the read replica faces difficulties keeping up with the increasing read traffic, causing performance bottlenecks during peak periods.

Which of the following will resolve the issue with the most cost-effective solution?

Use automatic scaling for the Aurora read replica using Aurora Auto Scaling.
Set up a read replica that can operate across different regions.
Implement read scaling with Aurora Global Database.
Increase the size of the Aurora DB cluster.
Correct
Amazon Aurora is a cloud-based relational database service that provides better performance and reliability for database workloads. It is highly available and scalable, making it a great choice for businesses of any size. One of the key features of Amazon Aurora is Aurora Auto Scaling, which automatically adjusts the capacity of your Aurora database cluster based on the workload. This means that you don’t have to worry about manually adjusting the ability of your database cluster to handle changes in demand. With Aurora Auto Scaling, you can be sure that your database cluster will always have the appropriate capacity to handle your workload while minimizing costs.

Amazon Aurora

Aurora Auto Scaling is particularly useful for businesses that have fluctuating workloads. It ensures that your database cluster scales up or down as needed without manual intervention. This feature saves time and resources, allowing businesses to focus on other aspects of their operations. Aurora Auto Scaling is also cost-effective, as it helps minimize unnecessary expenses associated with overprovisioning or underprovisioning database resources.

In this scenario, the company can benefit from using Aurora Auto Scaling. This solution allows the system to dynamically manage resources, effectively addressing the surge in read traffic during peak periods. This dynamic management of resources ensures that the company pays only for the extra resources when they are genuinely required.

Hence, the correct answer is: Use automatic scaling for the Aurora read replica using Aurora Auto Scaling.

The option that says: Increase the size of the Aurora DB cluster is incorrect because it’s not economical to upsize the cluster just to alleviate the bottleneck during peak periods. A static increase in the DB cluster size results in constant costs, regardless of whether your database’s resources are being fully utilized during off-peak periods or not.

The option that says: Implement read scaling with Aurora Global Database is incorrect. Amazon Aurora Global Database is primarily designed for globally distributed applications, allowing a single Amazon Aurora database to span multiple AWS Regions. While this can provide global availability, it introduces additional complexity and can be more expensive due to infrastructure and data transfer costs.

The option that says: Set up a read replica that can operate across different regions is incorrect. Setting up a read replica that operates across different regions can provide read scalability and load-balancing benefits by typically distributing the read traffic across regions. However, it is not the most cost-effective solution in this scenario since it incurs additional costs associated with inter-region data replication. Moreover, the issue is not related to cross-region availability but rather the read replica’s performance within the current region.

 

References:

https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Integrating.AutoScaling.html

https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html

 

Check out this Amazon Aurora Cheat Sheet:

https://tutorialsdojo.com/amazon-aurora/


9. Question
A Solutions Architect created a new Standard-class Amazon S3 bucket to store financial reports that are not frequently accessed but should immediately be available when an auditor requests the reports. To save costs, the Architect changed the storage class of the S3 bucket from Standard to Infrequent Access storage class.

In S3 Standard – Infrequent Access storage class, which of the following statements are true? (Select TWO.)

It is designed for data that is accessed less frequently.
It is designed for data that requires rapid access when needed.
Ideal to use for data archiving.
It automatically moves data to the most cost-effective access tier without any operational overhead.
It provides high latency and low throughput performance.
Correct
Amazon S3 Standard – Infrequent Access (Standard – IA) is an Amazon S3 storage class for data that is accessed less frequently, but requires rapid access when needed. Standard – IA offers the high durability, throughput, and low latency of Amazon S3 Standard, with a low per GB storage price and per GB retrieval fee.

Amazon S3 

This combination of low cost and high performance make Standard – IA ideal for long-term storage, backups, and as a data store for disaster recovery. The Standard – IA storage class is set at the object level and can exist in the same bucket as Standard, allowing you to use lifecycle policies to automatically transition objects between storage classes without any application changes.

Key Features:

– Same low latency and high throughput performance of Standard

– Designed for durability of 99.999999999% of objects

– Designed for 99.9% availability over a given year

– Backed with the Amazon S3 Service Level Agreement for availability

– Supports SSL encryption of data in transit and at rest

– Lifecycle management for automatic migration of objects

Hence, the correct answers are:

– It is designed for data that is accessed less frequently.

– It is designed for data that requires rapid access when needed.

The option that says: It automatically moves data to the most cost-effective access tier without any operational overhead is incorrect because it actually refers to Amazon S3 – Intelligent Tiering, which is the only cloud storage class that delivers automatic cost savings by moving objects between different access tiers when access patterns change.

The option that says: It provides high latency and low throughput performance is incorrect because it should just be “low latency” and “high throughput” instead. S3 automatically scales performance to meet user demands.

The option that says: Ideal to use for data archiving is incorrect because this statement refers to Amazon S3 Glacier. Glacier is a secure, durable, and extremely low-cost cloud storage service for data archiving and long-term backup.

 

References:

https://aws.amazon.com/s3/storage-classes/

https://aws.amazon.com/s3/faqs

 

Check out this Amazon S3 Cheat Sheet:

https://tutorialsdojo.com/amazon-s3/


10. Question
A startup is building IoT devices and monitoring applications. They are using IoT sensors to monitor the traffic in real-time by using an Amazon Kinesis Stream that is configured with default settings. It then sends the data to an Amazon S3 bucket every 3 days. When you checked the data in S3 on the 3rd day, only the data for the last day is present and no data is present from 2 days ago.

Which of the following is the MOST likely cause of this issue?

The access of the Kinesis stream to the S3 bucket is insufficient.
Someone has manually deleted the record in Amazon S3.
Amazon S3 bucket has encountered a data loss.
By default, data records in Kinesis are only accessible for 24 hours from the time they are added to a stream.
Correct
By default, records of a stream in Amazon Kinesis are accessible for up to 24 hours from the time they are added to the stream. You can raise this limit to up to 7 days by enabling extended data retention.



Hence, the correct answer is: By default, data records in Kinesis are only accessible for 24 hours from the time they are added to a stream.

The option that says: Amazon S3 bucket has encountered a data loss is incorrect because Amazon S3 rarely experiences data loss. Amazon has an SLA for S3 that it commits to its customers. Amazon S3 Standard, S3 Standard–IA, S3 One Zone-IA, and S3 Glacier are all designed to provide 99.999999999% durability of objects over a given year. This durability level corresponds to an average annual expected loss of 0.000000001% of objects. Hence, Amazon S3 bucket data loss is highly unlikely.

The option that says: Someone has manually deleted the record in Amazon S3 is incorrect because if someone has deleted the data, this should have been visible in CloudTrail. Also, deleting that much data manually shouldn’t have occurred in the first place if you have put in the appropriate security measures.

The option that says: The access of the Kinesis stream to the S3 bucket is insufficient is incorrect because having insufficient access is highly unlikely since you are able to access the bucket and view the contents of the previous day’s data collected by Kinesis.

 

Reference: 

https://aws.amazon.com/kinesis/data-streams/faqs/

https://docs.aws.amazon.com/AmazonS3/latest/dev/DataDurability.html

 

Check out this Amazon Kinesis Cheat Sheet:

https://tutorialsdojo.com/amazon-kinesis/


12. Question
A company is using Amazon VPC that has a CIDR block of 10.31.0.0/27 that is connected to the on-premises data center. There was a requirement to create a Lambda function that will process massive amounts of cryptocurrency transactions every minute and then store the results to EFS. After setting up the serverless architecture and connecting the Lambda function to the VPC, the Solutions Architect noticed an increase in invocation errors with EC2 error types such as EC2ThrottledException at certain times of the day.

Which of the following are the possible causes of this issue? (Select TWO.)

Your Lambda function exceeds the VPC quota for Elastic Network Interfaces (ENIs) or available IP addresses in the subnet.
The Lambda function is placed in a VPC subnet with limited IP address capacity.
Your VPC does not have a NAT gateway.
The attached IAM execution role of your function does not have the necessary permissions to access the resources of your VPC.
The associated security group of your function does not allow outbound connections.
Correct
Amazon VPC (Virtual Private Cloud) is a service that enables you to create a virtual network. This virtual network is logically isolated from other networks, giving you full control over your virtual networking environment. It allows you to choose your own IP address range, create subnets, and configure route tables and network gateways. With VPC, you can securely connect your AWS resources to your on-premises data center.



Elastic Network Interfaces (ENIs) are virtual network interfaces that can be attached to instances or Lambda functions within your VPC. When you configure a Lambda function to access resources within a VPC, AWS Lambda creates and manages ENIs on your behalf. These ENIs are required for communication between the Lambda function and resources such as Amazon EFS within the VPC. Properly configuring your VPC and ensuring you have enough IP addresses and ENI capacity is crucial for your Lambda function to scale effectively without encountering errors like EC2ThrottledException.

Service Quotas within Amazon VPC are important, especially when using AWS Lambda. As your Lambda function scales, it requires additional ENIs to maintain connectivity within the VPC. If your VPC reaches its quota limit for ENIs or IP addresses, your Lambda function may fail to scale, leading to invocation errors. Monitoring and adjusting these quotas and ensuring an optimal VPC configuration are essential to maintaining a stable and scalable serverless architecture.

Hence, the correct answers for this scenario are:

– Your Lambda function exceeds the VPC quota for Elastic Network Interfaces (ENIs) or available IP addresses in the subnet.

– The Lambda function is placed in a VPC subnet with limited IP address capacity.

The option that says: Your VPC does not have a NAT gateway is incorrect because an issue in the NAT Gateway is unlikely to cause a request throttling issue or produce an EC2ThrottledException error in Lambda. As per the scenario, the issue is happening only at certain times of the day, which means that the issue is only intermittent and the function works at other times. We can also conclude that an availability issue is not an issue since the application is already using a highly available NAT Gateway and not just a NAT instance.

The option that says: The associated security group of your function does not allow outbound connections is incorrect because if the associated security group does not allow outbound connections, then the Lambda function will not work at all in the first place. Remember that as per the scenario, the issue only happens intermittently. In addition, Internet traffic restrictions do not usually produce EC2ThrottledException errors.

The option that says: The attached IAM execution role of your function does not have the necessary permissions to access the resources of your VPC is incorrect because just as what is explained above, the issue is intermittent and thus, the IAM execution role of the function does have the necessary permissions to access the resources of the VPC since it works at those specific times. In case the issue is indeed caused by a permission problem, then an EC2AccessDeniedException the error would most likely be returned and not an EC2ThrottledException error.

 

References:

https://docs.aws.amazon.com/lambda/latest/dg/vpc.html

https://aws.amazon.com/premiumsupport/knowledge-center/internet-access-lambda-function/

https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html

 

Check out this AWS Lambda Cheat Sheet:

https://tutorialsdojo.com/aws-lambda/


13. Question
A company plans to implement a hybrid architecture. A dedicated connection needs to be created from the Amazon Virtual Private Cloud (VPC) to the on-premises network. This connection must provide high bandwidth throughput and a more consistent network experience than Internet-based solutions.

Which of the following can be used to create a private connection between the VPC and the company’s on-premises network?

AWS Site-to-Site VPN
Transit Gateway with equal-cost multipath routing (ECMP)
Transit VPC
AWS Direct Connect
Correct
AWS Direct Connect links your internal network to an AWS Direct Connect location over a standard Ethernet fiber-optic cable. One end of the cable is connected to your router, the other to an AWS Direct Connect router.

AWS Direct Connect diagram

With this connection, you can create virtual interfaces directly to public AWS services (for example, to Amazon S3) or to Amazon VPC, bypassing internet service providers in your network path. An AWS Direct Connect location provides access to AWS in the region with which it is associated. You can use a single connection in a public Region or AWS GovCloud (US) to access public AWS services in all other public Regions

Hence, the correct answer is: AWS Direct Connect.

Transit VPC is incorrect because this in itself is not enough to integrate your on-premises network to your VPC. You have to either use a VPN or a Direct Connect connection. A transit VPC is primarily used to connect multiple VPCs and remote networks in order to create a global network transit center and not for establishing a dedicated connection to your on-premises network.

Transit Gateway with equal-cost multipath routing (ECMP) is incorrect because a transit gateway is commonly used to connect multiple VPCs and on-premises networks through a central hub. Just like transit VPC, a transit gateway is not capable of establishing a direct and dedicated connection to your on-premises network.

AWS Site-to-Site VPN is incorrect because this type of connection traverses the public Internet. Moreover, it doesn’t provide a high bandwidth throughput and a more consistent network experience than Internet-based solutions.

 

References:

https://aws.amazon.com/premiumsupport/knowledge-center/connect-vpc/

https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html

 

Check out this AWS Direct Connect Cheat Sheet:

https://tutorialsdojo.com/aws-direct-connect/

 

Comparison of AWS Services Cheat Sheets:

https://tutorialsdojo.com/comparison-of-aws-services/
