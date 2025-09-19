```markdown
# Networking Costs in AWS  
# AWS에서의 네트워킹 비용  

🎮 게임보상: "AWS Networking Strategist" +550 XP  

---

## Networking Costs in AWS  
## AWS에서의 네트워킹 비용  

Let's discuss networking costs in AWS per gigabyte.  
AWS에서 기가바이트 단위로 네트워킹 비용을 살펴보겠습니다.  

This overview is simplified to explain a few important concepts clearly.  
이 개요는 몇 가지 중요한 개념을 명확히 설명하기 위해 단순화되었습니다.  

Networking costs can get very complicated, but this high-level summary should help you prepare for the exam.  
네트워킹 비용은 매우 복잡할 수 있지만, 이 요약은 시험 준비에 도움이 됩니다.  

---

## AWS Region and Availability Zones  
## AWS 리전 및 가용 영역(AZ)  

Consider a region with two availability zones (AZs).  
두 개의 가용 영역(AZ)이 있는 리전을 생각해봅시다.  

Suppose we have an EC2 instance in the first AZ.  
첫 번째 AZ에 EC2 인스턴스가 있다고 가정합니다.  

The first key point is that any incoming traffic to your EC2 instances is free.  
첫 번째 핵심 포인트는 EC2 인스턴스로 들어오는 트래픽은 무료라는 것입니다.  

That means all inbound traffic onto EC2 is free of charge.  
즉, EC2로 들어오는 모든 인바운드 트래픽은 비용이 부과되지 않습니다.  

Now, assume there is a second EC2 instance in the same availability zone.  
이제 같은 AZ에 두 번째 EC2 인스턴스가 있다고 가정합니다.  

Since an availability zone represents multiple data centers geographically close to each other, any traffic between these two EC2 instances will be free, provided they communicate using their private IP addresses.  
AZ는 지리적으로 가까운 여러 데이터센터를 나타내므로, 두 EC2 인스턴스가 프라이빗 IP를 사용해 통신하면 트래픽은 무료입니다.  

Using private IPs ensures the traffic stays within the connected network.  
프라이빗 IP를 사용하면 트래픽이 연결된 네트워크 내부에 머물게 됩니다.  

---

## Communication Across Availability Zones  
## 가용 영역 간 통신  

If we include an EC2 instance in another availability zone within the same region, and these two instances communicate, there are two options:  
같은 리전 내 다른 AZ에 있는 EC2 인스턴스와 통신할 경우 두 가지 옵션이 있습니다.  

Using a public IP or elastic IP, which costs 2 cents per gigabyte.  
퍼블릭 IP 또는 Elastic IP를 사용하면 GB당 2센트가 비용으로 발생합니다.  

Using a private IP, which costs half as much because the traffic uses the internal AWS network linking the two AZs.  
프라이빗 IP를 사용하면 비용이 절반으로 줄어들며, 이는 트래픽이 두 AZ를 연결하는 AWS 내부 네트워크를 사용하기 때문입니다.  

Therefore, to achieve faster communication and lower costs, use private IPs whenever possible instead of public IPs.  
따라서 더 빠른 통신과 낮은 비용을 위해 가능하면 퍼블릭 IP 대신 프라이빗 IP를 사용하세요.  

---

## Communication Between Different Regions  
## 다른 리전 간 통신  

When traffic flows between different AWS regions, the cost is 2 cents per gigabyte.  
서로 다른 AWS 리전 간 트래픽은 GB당 2센트의 비용이 발생합니다.  

This inter-region traffic can be quite expensive, so it's important to consider this when designing your architecture.  
리전 간 트래픽은 상당히 비쌀 수 있으므로, 아키텍처 설계 시 이를 고려하는 것이 중요합니다.  

---

## Summary of Networking Cost Takeaways  
## 네트워킹 비용 요약  

Use private IPs instead of public IPs to save costs and improve network performance within the same region.  
같은 리전 내에서는 비용 절감과 성능 향상을 위해 퍼블릭 IP 대신 프라이빗 IP를 사용하세요.  

For clusters requiring extensive communication between EC2 instances, placing instances in the same availability zone maximizes cost savings.  
EC2 인스턴스 간 통신이 많은 클러스터의 경우, 인스턴스를 같은 AZ에 배치하면 비용 절감 효과가 최대화됩니다.  

However, this cost saving reduces high availability since if the AZ goes down, there is no failover.  
하지만 비용 절감은 고가용성을 낮추므로, AZ가 다운되면 페일오버가 없습니다.  

You must balance high availability and cost based on your requirements.  
요구 사항에 따라 고가용성과 비용 사이의 균형을 맞춰야 합니다.  

For example, creating an RDS read replica in the same AZ incurs no network cost, but creating it in another AZ costs 1 cent per gigabyte of data transfer.  
예를 들어, RDS 읽기 전용 복제본을 같은 AZ에 생성하면 네트워크 비용이 없지만, 다른 AZ에 생성하면 GB당 1센트의 데이터 전송 비용이 발생합니다.  

---

## Optimizing Networking Costs with Architectural Decisions  
## 아키텍처 설계를 통한 네트워킹 비용 최적화  

Egress traffic refers to outbound traffic from AWS to the outside, while ingress traffic is inbound traffic from outside to AWS, which is typically free.  
Egress 트래픽은 AWS에서 외부로 나가는 트래픽이고, Ingress 트래픽은 외부에서 AWS로 들어오는 트래픽으로 일반적으로 무료입니다.  

Sending data to AWS usually costs nothing, but taking data outside AWS incurs charges.  
AWS로 데이터를 보내는 것은 대부분 무료이지만, AWS 밖으로 데이터를 내보내면 비용이 발생합니다.  

Your goal should be to keep as much internet traffic as possible within AWS to minimize costs.  
비용을 최소화하려면 가능한 많은 인터넷 트래픽을 AWS 내부에 유지하는 것이 목표여야 합니다.  

Consider a scenario where a database is in AWS and a user runs an application in a corporate data center.  
데이터베이스가 AWS에 있고 사용자가 기업 데이터 센터에서 애플리케이션을 실행하는 상황을 고려해봅시다.  

The application queries the database and retrieves 100 megabytes of data, performs aggregation and computation, and returns only 50 kilobytes to the user.  
애플리케이션이 데이터베이스에서 100MB 데이터를 조회하여 집계 및 계산 후 50KB만 사용자에게 반환합니다.  

Here, the egress traffic is very high because 100 megabytes are transferred out of AWS to the corporate data center, incurring significant costs.  
이 경우 100MB가 AWS 밖으로 전송되므로 Egress 트래픽이 높아 비용이 많이 발생합니다.  

A smarter approach is to move the application into AWS, for example, on an EC2 instance in the same availability zone as the database.  
더 효율적인 방법은 애플리케이션을 AWS 내부, 예를 들어 데이터베이스와 같은 AZ의 EC2 인스턴스로 이동하는 것입니다.  

In this case, the 100 megabytes of data transfer within the AZ is free, and only the 50 kilobytes of query results are sent outside, greatly reducing egress costs.  
이 경우 AZ 내 데이터 전송 100MB는 무료이며, 50KB 결과만 외부로 전송되어 Egress 비용이 크게 줄어듭니다.  

If you use AWS Direct Connect, choose a Direct Connect location co-located in the same AWS region to minimize egress network costs.  
AWS Direct Connect를 사용할 경우, 동일 리전에 있는 Direct Connect 위치를 선택하여 Egress 네트워크 비용을 최소화하세요.  

---

## Amazon S3 Data Transfer Pricing (USA Example)  
## Amazon S3 데이터 전송 요금 (미국 예시)  

Data ingress into an S3 bucket is free.  
S3 버킷으로 들어오는 데이터(Ingress)는 무료입니다.  

Downloading data from S3 to your computer over the internet costs 9 cents per gigabyte.  
S3에서 인터넷을 통해 데이터를 다운로드하는 경우 GB당 9센트가 발생합니다.  

Using S3 Transfer Acceleration to speed up transfers (50 to 500% faster) adds an additional cost between 4 to 8 cents per gigabyte.  
S3 Transfer Acceleration으로 전송 속도를 높이면(50~500% 빠름) GB당 4~8센트 추가 비용이 발생합니다.  

Data transfer between S3 and CloudFront is free.  
S3와 CloudFront 간 데이터 전송은 무료입니다.  

Data transfer from CloudFront to the internet costs 8.5 cents per gigabyte, which is slightly cheaper than direct S3 internet transfer.  
CloudFront에서 인터넷으로 전송할 경우 GB당 8.5센트로, 직접 S3 인터넷 전송보다 약간 저렴합니다.  

CloudFront also provides caching capabilities, reducing latency and request costs.  
CloudFront는 캐싱 기능도 제공하여 지연 시간과 요청 비용을 줄입니다.  

Requests to S3 incur costs, but requests to CloudFront are about seven times cheaper.  
S3 요청은 비용이 발생하지만, CloudFront 요청은 약 7배 저렴합니다.  

Cross-region replication for S3 buckets costs 2 cents per gigabyte.  
S3 버킷 간 리전 복제는 GB당 2센트가 발생합니다.  

---

## NAT Gateway vs. Gateway VPC Endpoint  
## NAT 게이트웨이 vs VPC 게이트웨이 엔드포인트  

Consider a VPC with two private subnets containing EC2 instances that need to access data in an Amazon S3 bucket.  
S3 데이터에 접근해야 하는 EC2 인스턴스가 있는 두 개의 프라이빗 서브넷을 가진 VPC를 생각해봅시다.  

Using a NAT Gateway involves setting up a public subnet with a route to an Internet Gateway.  
NAT 게이트웨이를 사용하는 경우, 인터넷 게이트웨이 경로가 있는 퍼블릭 서브넷을 설정해야 합니다.  

Traffic flows from the EC2 instances through the NAT Gateway and Internet Gateway to the internet to access S3.  
트래픽은 EC2 인스턴스에서 NAT 게이트웨이와 인터넷 게이트웨이를 거쳐 인터넷을 통해 S3에 접근합니다.  

Costs for NAT Gateway include:  
NAT 게이트웨이 비용은 다음과 같습니다.  

- $0.045 per hour for the NAT Gateway.  
- NAT 게이트웨이 시간당 $0.045  

- $0.045 per gigabyte of data processed through the NAT Gateway.  
- NAT 게이트웨이를 통해 처리된 데이터 GB당 $0.045  

- 0.09 per gigabyte for data transfer out to S3 cross-region (or 0 if same region).  
- S3 다른 리전으로 전송 시 GB당 $0.09 (같은 리전이면 무료)  

Using a VPC Gateway Endpoint allows private connectivity directly from the private subnets to S3 without traversing the internet.  
VPC 게이트웨이 엔드포인트를 사용하면 인터넷을 거치지 않고 프라이빗 서브넷에서 S3로 프라이빗 연결이 가능합니다.  

Costs for Gateway Endpoint include:  
게이트웨이 엔드포인트 비용은 다음과 같습니다.  

- No hourly charge.  
- 시간당 비용 없음  

- $0.01 per gigabyte of data transferred in and out of S3 within the same region.  
- 같은 리전 내 S3 데이터 전송 GB당 $0.01  

Using a VPC Endpoint can significantly reduce costs compared to a NAT Gateway, which is an important consideration for the exam.  
VPC 엔드포인트를 사용하면 NAT 게이트웨이 대비 비용을 크게 줄일
```


수 있으며, 이는 시험에서 중요한 고려 사항입니다.

---

## Conclusion

## 결론

Understanding AWS networking costs and making smart architectural decisions can optimize your expenses and improve performance.
AWS 네트워킹 비용을 이해하고 현명한 아키텍처 결정을 내리면 비용 최적화와 성능 향상이 가능합니다.

Use private IPs for intra-region communication, keep traffic within availability zones when possible, leverage VPC Endpoints for private S3 access, and carefully consider data transfer costs across regions and services.
리전 내 통신에는 프라이빗 IP를 사용하고, 가능하면 AZ 내에서 트래픽을 유지하며, 프라이빗 S3 접근에는 VPC 엔드포인트를 활용하고, 리전 및 서비스 간 데이터 전송 비용을 신중히 고려하세요.

---

## Key Takeaways

## 핵심 요약

* Incoming traffic to EC2 instances is free, and traffic between instances in the same availability zone using private IPs is also free.

* EC2 인스턴스로 들어오는 트래픽은 무료이며, 같은 AZ 내 프라이빗 IP를 사용한 인스턴스 간 트래픽도 무료입니다.

* Using private IPs for communication between instances in different availability zones within the same region costs half as much as using public or elastic IPs.

* 같은 리전 내 다른 AZ 인스턴스 간 통신은 퍼블릭/Elastic IP 대비 비용이 절반입니다.

* Data transfer between different AWS regions incurs higher costs, so architectural decisions should balance cost and availability.

* 다른 리전 간 데이터 전송은 비용이 높으므로, 아키텍처 설계 시 비용과 가용성의 균형을 고려해야 합니다.

* Utilizing VPC Gateway Endpoints for S3 access is significantly cheaper than using NAT Gateways, reducing data transfer costs.

* S3 접근 시 VPC 게이트웨이 엔드포인트를 사용하면 NAT 게이트웨이보다 훨씬 저렴하여 데이터 전송 비용을 줄일 수 있습니다.

```

원하면, 내가 이 내용을 **더 보기 좋게 요약된 표 형태의 md 버전**으로도 만들어서 핵심 비용 비교까지 한눈에 보이게 할 수 있어. 만들까?
```
