```markdown
# VPC Endpoints  
# VPC 엔드포인트  

🎮 게임보상: "Private Access Key" +500 XP  

---

## Introduction to VPC Endpoints  
## VPC 엔드포인트 소개  

Let's discuss VPC endpoints.  
VPC 엔드포인트에 대해 알아보겠습니다.  

The idea is that AWS services such as DynamoDB are publicly accessible.  
DynamoDB와 같은 AWS 서비스는 기본적으로 공개 접근이 가능합니다.  

This means your entire infrastructure accesses DynamoDB through your NAT gateway and internet gateway, or directly through your internet gateway.  
즉, 전체 인프라는 NAT 게이트웨이와 인터넷 게이트웨이를 통해, 또는 인터넷 게이트웨이를 직접 통해 DynamoDB에 접근합니다.  

However, all this traffic goes through the public internet.  
하지만 모든 트래픽이 공개 인터넷을 통과합니다.  

---

You may have other services such as CloudWatch and Amazon S3 that you want to access privately, without going through the internet.  
CloudWatch나 Amazon S3와 같은 다른 서비스를 인터넷을 거치지 않고 사설로 접근하고 싶을 수 있습니다.  

To achieve this, you use VPC endpoints so your instances do not have to traverse the public internet.  
이를 위해 VPC 엔드포인트를 사용하면 인스턴스가 공개 인터넷을 거치지 않아도 됩니다.  

Instead, they can connect directly through the private AWS network to these services.  
대신, 사설 AWS 네트워크를 통해 해당 서비스에 직접 연결할 수 있습니다.  

---

## VPC Endpoint Architecture  
## VPC 엔드포인트 아키텍처  

Consider a familiar architecture with public subnets containing a NAT gateway and EC2 instances, and private subnets with EC2 instances.  
NAT 게이트웨이와 EC2 인스턴스가 있는 퍼블릭 서브넷, 그리고 EC2 인스턴스가 있는 프라이빗 서브넷 구조를 생각해봅시다.  

An internet gateway allows access to AWS services such as Amazon SNS through various paths.  
인터넷 게이트웨이를 통해 Amazon SNS와 같은 AWS 서비스에 다양한 경로로 접근할 수 있습니다.  

For example, an EC2 instance in a private subnet accesses Amazon SNS by routing through the NAT gateway, then the internet gateway, and finally to the Amazon SNS service publicly.  
예를 들어, 프라이빗 서브넷의 EC2 인스턴스는 NAT 게이트웨이, 인터넷 게이트웨이를 거쳐 Amazon SNS에 공개적으로 접근합니다.  

Similarly, an EC2 instance in a public subnet accesses Amazon SNS directly through the internet gateway.  
마찬가지로, 퍼블릭 서브넷의 EC2 인스턴스는 인터넷 게이트웨이를 통해 SNS에 직접 접근합니다.  

---

While this approach works, it incurs costs because the NAT gateway charges fees.  
이 방법은 작동하지만 NAT 게이트웨이 요금이 발생하여 비용이 듭니다.  

The internet gateway itself does not have a cost, but the multiple hops make this method inefficient.  
인터넷 게이트웨이는 비용이 없지만, 여러 홉을 거치므로 효율적이지 않습니다.  

Instead, you can use a VPC endpoint deployed within your VPC.  
대신, VPC 내에 배치된 VPC 엔드포인트를 사용할 수 있습니다.  

By configuring networking appropriately, the EC2 instance in the private subnet can route through the VPC endpoint directly to the Amazon SNS service.  
네트워킹을 적절히 구성하면, 프라이빗 서브넷의 EC2 인스턴스가 VPC 엔드포인트를 통해 SNS에 직접 접근할 수 있습니다.  

This keeps the network traffic entirely within AWS, which is highly beneficial.  
이로 인해 네트워크 트래픽이 AWS 내부에만 존재하게 되어 매우 유리합니다.  

---

## AWS PrivateLink and VPC Endpoints  
## AWS PrivateLink와 VPC 엔드포인트  

Every AWS service is publicly exposed with a public URL.  
모든 AWS 서비스는 공개 URL로 공개되어 있습니다.  

When you use VPC endpoints, they are powered by AWS PrivateLink, enabling private access to these services over the AWS network instead of the public internet.  
VPC 엔드포인트를 사용하면 AWS PrivateLink가 제공되어, 공개 인터넷 대신 AWS 네트워크를 통해 사설로 서비스에 접근할 수 있습니다.  

These VPC endpoints are redundant and scale horizontally.  
이 VPC 엔드포인트는 중복 구성이 가능하며 수평적으로 확장됩니다.  

They eliminate the need for an internet gateway or NAT gateway to access AWS services, significantly simplifying your network infrastructure.  
AWS 서비스 접근 시 인터넷 게이트웨이 또는 NAT 게이트웨이가 필요 없어 네트워크 인프라가 크게 단순화됩니다.  

In case of connectivity issues, you should check the DNS resolution settings in your VPC and your route tables.  
연결 문제가 발생하면 VPC의 DNS 설정과 라우트 테이블을 확인해야 합니다.  

---

## Types of VPC Endpoints  
## VPC 엔드포인트 유형  

There are two types of VPC endpoints:  
VPC 엔드포인트에는 두 가지 유형이 있습니다.  

- Interface Endpoints: Powered by PrivateLink, these provision an Elastic Network Interface (ENI) with a private IP address in your VPC. This ENI acts as an entry point to the private AWS service.  
- 인터페이스 엔드포인트: PrivateLink 기반으로, VPC에 사설 IP를 가진 ENI(Elastic Network Interface)를 생성합니다. 이 ENI가 사설 AWS 서비스의 진입점 역할을 합니다.  

- Gateway Endpoints: These provision a gateway that you specify as a target in your route table. They do not use IP addresses or security groups.  
- 게이트웨이 엔드포인트: 라우트 테이블의 대상으로 지정할 수 있는 게이트웨이를 생성하며, IP 주소나 보안 그룹을 사용하지 않습니다.  

---

## Interface Endpoints  
## 인터페이스 엔드포인트  

Interface Endpoints require attaching a security group because they provision an ENI.  
인터페이스 엔드포인트는 ENI를 생성하므로 보안 그룹을 연결해야 합니다.  

They support most AWS services, if not all.  
거의 대부분의 AWS 서비스를 지원합니다.  

However, they incur costs based on hourly usage and data processed.  
하지만 시간 단위 사용량과 처리 데이터에 따라 비용이 발생합니다.  

For example, an EC2 instance in a private subnet can access a service through an Interface Endpoint ENI, leveraging PrivateLink.  
예를 들어, 프라이빗 서브넷의 EC2 인스턴스가 PrivateLink를 활용해 인터페이스 엔드포인트 ENI를 통해 서비스에 접근할 수 있습니다.  

This method works for virtually every AWS service.  
이 방법은 사실상 모든 AWS 서비스에 적용 가능합니다.  

---

## Gateway Endpoints  
## 게이트웨이 엔드포인트  

Gateway Endpoints provision a gateway used as a target in a route table.  
게이트웨이 엔드포인트는 라우트 테이블의 대상으로 사용되는 게이트웨이를 생성합니다.  

They do not use IP addresses or security groups.  
IP 주소나 보안 그룹을 사용하지 않습니다.  

There are only two services supported by Gateway Endpoints: Amazon S3 and DynamoDB.  
게이트웨이 엔드포인트는 Amazon S3와 DynamoDB 두 서비스만 지원합니다.  

The advantage of Gateway Endpoints is that they are free and scale automatically because they only involve route table access.  
게이트웨이 엔드포인트의 장점은 무료이며, 라우트 테이블 접근만 포함되어 자동으로 확장됩니다.  

In this setup, you provide a Gateway Endpoint in your VPC and gain access to Amazon S3 or DynamoDB without additional cost.  
이 구성에서는 VPC에 게이트웨이 엔드포인트를 제공하면 추가 비용 없이 S3나 DynamoDB에 접근할 수 있습니다.  

---

## Choosing Between Interface and Gateway Endpoints for Amazon S3 and DynamoDB  
## Amazon S3와 DynamoDB에서 인터페이스와 게이트웨이 엔드포인트 선택  

You might wonder whether to use an Interface Endpoint or a Gateway Endpoint for Amazon S3 or DynamoDB, since both are options.  
S3나 DynamoDB에서는 인터페이스 엔드포인트와 게이트웨이 엔드포인트 중 어느 것을 선택해야 하는지 궁금할 수 있습니다.  

Generally, the Gateway Endpoint is preferred, especially in exam scenarios, because it only requires modifying a route table.  
일반적으로 게이트웨이 엔드포인트가 선호되며, 특히 시험 시나리오에서는 라우트 테이블 수정만 필요하기 때문입니다.  

It is free and scales better.  
무료이며 더 잘 확장됩니다.  

The Interface Endpoint incurs costs.  
인터페이스 엔드포인트는 비용이 발생합니다.  

The Interface Endpoint may be preferable if you require private access from on-premises environments, such as your data center, using site-to-site VPN or Direct Connect.  
인터페이스 엔드포인트는 온프레미스 환경(데이터센터 등)에서 VPN 또는 Direct Connect를 통해 사설 접근이 필요한 경우 선호될 수 있습니다.  

It may also be useful if you want to connect from another VPC through the Interface Endpoint.  
또한 다른 VPC에서 인터페이스 엔드포인트를 통해 연결하려는 경우에도 유용합니다.  

These are advanced use cases.  
이러한 경우는 고급 사용 사례입니다.  

Most of the time, the Gateway Endpoint is the preferred solution for Amazon S3.  
대부분의 경우 S3에는 게이트웨이 엔드포인트가 선호됩니다.  

---

## Conclusion  
## 결론  

That concludes this lecture on VPC endpoints.  
이로써 VPC 엔드포인트에 대한 강의를 마칩니다.  

I hope you found it informative, and I look forward to seeing you in the next lecture.  
유익한 내용이었기를 바라며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- VPC endpoints allow private access to AWS services without traversing the public internet.  
- VPC 엔드포인트를 사용하면 공개 인터넷을 거치지 않고 AWS 서비스에 사설 접근이 가능합니다.  

- There are two types of VPC endpoints: Interface Endpoints (powered by AWS PrivateLink) and Gateway Endpoints.  
- VPC 엔드포인트에는 인터페이스 엔드포인트(AWS PrivateLink 기반)와 게이트웨이 엔드포인트 두 가지가 있습니다.  

- Gateway Endpoints are free, scale automatically, and are used exclusively for Amazon S3 and DynamoDB.  
- 게이트웨이 엔드포인트는 무료이며 자동 확장되고, S3와 DynamoDB 전용으로 사용됩니다.  

- Interface Endpoints support most AWS services, require security groups, and incur hourly and data processing costs.  
- 인터페이스 엔드포인트는 대부분의 AWS 서비스를 지원하며, 보안 그룹이 필요하고 시간 단위 및 데이터 처리 비용이 발생합니다.

```
```
