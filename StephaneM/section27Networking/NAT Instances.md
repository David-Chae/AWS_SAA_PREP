```markdown
# NAT Instances  
# NAT 인스턴스  

🎮 게임보상: "Private Subnet Connector" +300 XP  

---

## Introduction to NAT Instances  
## NAT 인스턴스 소개  

Network Address Translation (NAT) instances are a method that allows EC2 instances in private subnets to connect to the internet.  
네트워크 주소 변환(NAT) 인스턴스는 프라이빗 서브넷의 EC2 인스턴스가 인터넷에 연결할 수 있게 해주는 방법입니다.  

Although NAT instances are considered outdated and have been largely replaced by NAT gateways, they may still appear on exams.  
NAT 인스턴스는 구식으로 간주되며 대부분 NAT 게이트웨이로 대체되었지만, 시험에서는 여전히 등장할 수 있습니다.  

This section explores how NAT instances function.  
이 섹션에서는 NAT 인스턴스가 어떻게 작동하는지 살펴봅니다.  

---

## NAT instances must be launched within a public subnet.  
## NAT 인스턴스는 반드시 퍼블릭 서브넷에 생성해야 합니다.  

They serve as a bridge connecting the public subnet with private subnets.  
퍼블릭 서브넷과 프라이빗 서브넷을 연결하는 브리지 역할을 합니다.  

To enable this functionality, a setting called the source/destination check must be disabled on the NAT instance, which will be demonstrated in the hands-on section.  
이 기능을 활성화하려면 NAT 인스턴스에서 source/destination 체크를 비활성화해야 합니다. (실습에서 보여줍니다)  

Additionally, the NAT instance requires a fixed Elastic IP address attached to it.  
또한 NAT 인스턴스에는 고정 Elastic IP 주소를 할당해야 합니다.  

---

## How NAT Instances Enable Connectivity  
## NAT 인스턴스가 연결을 가능하게 하는 방법  

Consider a public server with the IP address 50.60.4.10.  
IP 주소가 50.60.4.10인 퍼블릭 서버를 예로 들어보겠습니다.  

The goal is to access this server from EC2 instances located in private subnets.  
목표는 프라이빗 서브넷의 EC2 인스턴스에서 이 서버에 접근하는 것입니다.  

To establish this connectivity, a NAT instance is launched in a public subnet with its own security group.  
이 연결을 위해 NAT 인스턴스를 퍼블릭 서브넷에 생성하고, 자체 보안 그룹을 설정합니다.  

An Elastic IP is attached to this NAT instance.  
이 NAT 인스턴스에 Elastic IP를 할당합니다.  

Subsequently, the route tables for the private subnet are edited to allow traffic from the EC2 instances in the private subnet to route through the NAT instance in the public subnet.  
그 후, 프라이빗 서브넷의 라우트 테이블을 수정하여 프라이빗 서브넷의 EC2 트래픽이 퍼블릭 서브넷의 NAT 인스턴스를 통해 라우팅되도록 합니다.  

---

When an EC2 instance in the private subnet attempts to access the public server, the request originates with a source IP of 10.0.0.20, which is a private IP address, and a destination IP of 50.60.4.10.  
프라이빗 서브넷의 EC2 인스턴스가 퍼블릭 서버에 접근하려고 하면, 요청은 소스 IP 10.0.0.20(프라이빗 IP)과 목적지 IP 50.60.4.10으로 시작됩니다.  

The NAT instance intercepts this request and recognizes that it needs to forward the traffic to the public server.  
NAT 인스턴스는 이 요청을 가로채어 퍼블릭 서버로 전달해야 함을 인식합니다.  

It rewrites the source IP address of the packet to its own public Elastic IP, for example, 12.34.56.78.  
패킷의 소스 IP를 자신의 퍼블릭 Elastic IP(예: 12.34.56.78)로 변경합니다.  

This process is known as network packet rewriting, which is the core function of NAT.  
이 과정을 네트워크 패킷 재작성이라고 하며, NAT의 핵심 기능입니다.  

---

The public server receives the packet with the destination IP as 50.60.4.10 and the source IP as 12.34.56.78 (the NAT instance's public IP).  
퍼블릭 서버는 목적지 IP 50.60.4.10과 소스 IP 12.34.56.78(NAT 인스턴스의 퍼블릭 IP)로 패킷을 받습니다.  

When the server replies, it sends the response back to the NAT instance's public IP.  
서버가 응답하면 NAT 인스턴스의 퍼블릭 IP로 되돌려 보냅니다.  

The NAT instance then forwards the response back to the original EC2 instance in the private subnet, rewriting the destination IP back to the private IP 10.0.0.20.  
NAT 인스턴스는 응답을 프라이빗 IP 10.0.0.20로 다시 변경하여 원래 EC2 인스턴스로 전달합니다.  

This bidirectional rewriting enables seamless communication between private instances and the internet.  
이 양방향 IP 재작성으로 프라이빗 인스턴스와 인터넷 간의 원활한 통신이 가능합니다.  

---

Because the NAT instance modifies the source and destination IP addresses of packets, the source/destination check must be disabled on the NAT instance.  
NAT 인스턴스가 패킷의 소스와 목적지 IP를 변경하기 때문에 source/destination 체크를 비활성화해야 합니다.  

This allows the NAT instance to forward traffic that is not explicitly addressed to itself, which is essential for its operation.  
이 설정으로 NAT 인스턴스가 자신을 대상으로 하지 않은 트래픽도 전달할 수 있으며, 이는 NAT 작동에 필수적입니다.  

---

## Summary of NAT Instance Setup  
## NAT 인스턴스 설정 요약  

To summarize, setting up a NAT instance involves the following steps:  
요약하면, NAT 인스턴스를 설정하는 단계는 다음과 같습니다.  

1. Launch the NAT instance within a public subnet.  
1. 퍼블릭 서브넷에 NAT 인스턴스를 생성합니다.  

2. Attach a fixed Elastic IP address to the NAT instance.  
2. NAT 인스턴스에 고정 Elastic IP를 할당합니다.  

3. Modify the route tables of private subnets to route internet-bound traffic through the NAT instance.  
3. 프라이빗 서브넷의 라우트 테이블을 수정하여 인터넷 트래픽을 NAT 인스턴스를 통해 라우팅합니다.  

4. Disable the source/destination check on the NAT instance to allow packet forwarding.  
4. NAT 인스턴스에서 source/destination 체크를 비활성화하여 패킷 전달을 허용합니다.  

This setup enables EC2 instances in private subnets to access the internet via the NAT instance.  
이 설정으로 프라이빗 서브넷의 EC2 인스턴스가 NAT 인스턴스를 통해 인터넷에 접근할 수 있습니다.  

---

## Considerations and Limitations of NAT Instances  
## NAT 인스턴스 고려 사항 및 제한  

Amazon provides a pre-configured Amazon Linux AMI for NAT instances.  
Amazon은 NAT 인스턴스용 사전 구성된 Amazon Linux AMI를 제공합니다.  

However, this AMI reached its end of standard support on December 31st, 2020.  
하지만 이 AMI는 2020년 12월 31일부로 표준 지원이 종료되었습니다.  

Consequently, NAT gateways are now the recommended solution for providing internet access to private subnets.  
따라서 프라이빗 서브넷 인터넷 접근을 위해 NAT 게이트웨이가 권장됩니다.  

NAT instances are not highly available or resilient by default.  
NAT 인스턴스는 기본적으로 고가용성이나 내결함성을 제공하지 않습니다.  

To achieve high availability, multiple NAT instances must be deployed across multiple Availability Zones, potentially managed by an Auto Scaling Group with a resilient user-data script.  
고가용성을 위해서는 여러 AZ에 NAT 인스턴스를 배포하고, 내결함성 user-data 스크립트와 함께 Auto Scaling 그룹으로 관리해야 합니다.  

This setup can be complex.  
이 구성은 복잡할 수 있습니다.  

Additionally, the bandwidth available to a NAT instance depends on the instance size; smaller instances provide less bandwidth than larger ones.  
또한 NAT 인스턴스의 대역폭은 인스턴스 크기에 따라 달라집니다. 작은 인스턴스는 대역폭이 제한적입니다.  

Security groups and rules must be managed manually on the NAT instance, including allowing inbound HTTP and HTTPS traffic from private subnets and possibly SSH access from trusted networks.  
보안 그룹과 규칙은 NAT 인스턴스에서 수동으로 관리해야 하며, 프라이빗 서브넷에서 들어오는 HTTP/HTTPS와 신뢰된 네트워크에서의 SSH 접근을 허용해야 할 수 있습니다.  

Outbound traffic rules must also be configured appropriately.  
아웃바운드 트래픽 규칙도 적절히 구성해야 합니다.  

---

## Conclusion  
## 결론  

While NAT instances effectively demonstrate how network address translation works at a high level, they are being phased out in favor of NAT gateways, which provide a more scalable and manageable solution.  
NAT 인스턴스는 네트워크 주소 변환 작동을 보여주지만, 더 확장 가능하고 관리하기 쉬운 NAT 게이트웨이로 점차 대체되고 있습니다.  

The next lecture will cover NAT gateways in detail.  
다음 강의에서는 NAT 게이트웨이를 자세히 다룹니다.  

It is important to understand the differences between NAT instances and NAT gateways, especially for exam purposes.  
특히 시험 대비를 위해 NAT 인스턴스와 NAT 게이트웨이의 차이를 이해하는 것이 중요합니다.  

---

## Key Takeaways  
## 핵심 요약  

- NAT instances enable EC2 instances in private subnets to access the internet by routing traffic through a NAT instance in a public subnet.  
- NAT 인스턴스는 퍼블릭 서브넷의 NAT 인스턴스를 통해 트래픽을 라우팅하여 프라이빗 서브넷 EC2 인스턴스가 인터넷에 접근할 수 있게 합니다.  

- The NAT instance rewrites the source IP address of outgoing packets to its own Elastic IP, allowing return traffic to be routed correctly.  
- NAT 인스턴스는 아웃바운드 패킷의 소스 IP
```


를 자신의 Elastic IP로 변경하여 응답 트래픽이 올바르게 라우팅되도록 합니다.

* Source/destination checks must be disabled on the NAT instance to allow it to forward traffic properly.

* NAT 인스턴스에서 source/destination 체크를 비활성화해야 트래픽 전달이 올바르게 이루어집니다.

* NAT instances are outdated, not highly available by default, and require manual management; NAT gateways are the recommended modern solution.

* NAT 인스턴스는 구식이며 기본적으로 고가용성을 제공하지 않고 수동 관리가 필요합니다. 현대적인 솔루션으로는 NAT 게이트웨이가 권장됩니다.

```
```
