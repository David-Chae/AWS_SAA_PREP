
```markdown
# Egress Only Internet Gateway  
# Egress Only 인터넷 게이트웨이  

🎮 게임보상: "Egress-Only Gateway Explorer Badge" +600 XP  

---

## Introduction to Egress-Only Internet Gateways  
## Egress-Only 인터넷 게이트웨이 소개  

Egress-only internet gateways are used exclusively for IPv6 traffic.  
Egress-only 인터넷 게이트웨이는 오직 IPv6 트래픽만을 위해 사용됩니다.  

They are similar to NAT gateways, but while NAT gateways operate for IPv4, egress-only internet gateways are designed specifically for IPv6.  
NAT 게이트웨이와 유사하지만, NAT 게이트웨이가 IPv4용인 반면, egress-only 인터넷 게이트웨이는 IPv6 전용으로 설계되었습니다.  

These gateways allow instances within your Virtual Private Cloud (VPC) to establish outbound connections over IPv6.  
이 게이트웨이는 VPC 내 인스턴스가 IPv6를 통해 아웃바운드 연결을 수행할 수 있도록 합니다.  

However, they prevent the internet from initiating any IPv6 connections to your instances.  
그러나 인터넷이 인스턴스로 인바운드 IPv6 연결을 시작하는 것은 차단합니다.  

To enable this functionality, you must update your route tables accordingly.  
이 기능을 활성화하려면 라우트 테이블을 적절히 업데이트해야 합니다.  

---

## Example Scenario  
## 예제 시나리오  

Consider a VPC with both public and private subnets.  
퍼블릭 서브넷과 프라이빗 서브넷이 모두 있는 VPC를 생각해봅시다.  

An EC2 instance in a public subnet can access the internet through an internet gateway.  
퍼블릭 서브넷에 있는 EC2 인스턴스는 인터넷 게이트웨이를 통해 인터넷에 접근할 수 있습니다.  

Moreover, the internet can initiate connections to this instance over IPv6 because it is connected to the internet gateway and resides in a public subnet.  
게다가, 인터넷은 이 인스턴스가 퍼블릭 서브넷에 있고 인터넷 게이트웨이에 연결되어 있으므로 IPv6로 인바운드 연결을 시작할 수 있습니다.  

However, if you want to restrict inbound connections and allow only outbound connections, you would place the EC2 instance in a private subnet without an internet gateway.  
하지만 인바운드 연결을 제한하고 아웃바운드 연결만 허용하려면, 인터넷 게이트웨이가 없는 프라이빗 서브넷에 EC2 인스턴스를 배치해야 합니다.  

Instead, you create an egress-only internet gateway.  
대신 egress-only 인터넷 게이트웨이를 생성합니다.  

This setup enables the instance to access the internet over IPv6 through the egress-only internet gateway, while preventing the internet from initiating connections to the instance.  
이 구성은 인스턴스가 egress-only 인터넷 게이트웨이를 통해 IPv6로 인터넷에 접근할 수 있도록 하면서, 인터넷에서 인스턴스로 연결을 시작하는 것을 차단합니다.  

---

## IPv6 Routing Overview  
## IPv6 라우팅 개요  

Let's summarize how IPv6 routing works within a VPC that has both public and private subnets, each with IPv4 and IPv6 addressing.  
IPv4와 IPv6 주소를 모두 가진 퍼블릭 및 프라이빗 서브넷이 있는 VPC에서 IPv6 라우팅이 어떻게 작동하는지 요약해봅시다.  

For a web server in a public subnet, it can access the internet over both IPv4 and IPv6 through an internet gateway.  
퍼블릭 서브넷에 있는 웹 서버는 인터넷 게이트웨이를 통해 IPv4와 IPv6 모두로 인터넷에 접근할 수 있습니다.  

The route table for the public subnet includes entries for local IPv4 and IPv6 traffic within the VPC's CIDRs.  
퍼블릭 서브넷의 라우트 테이블에는 VPC CIDR 내 로컬 IPv4 및 IPv6 트래픽 항목이 포함됩니다.  

Additionally, it routes all other IPv4 traffic (0.0.0.0/0) and all IPv6 traffic (::/0) through the internet gateway, allowing full internet access.  
또한, 다른 모든 IPv4 트래픽(0.0.0.0/0)과 IPv6 트래픽(::/0)을 인터넷 게이트웨이로 라우팅하여 전체 인터넷 접근을 허용합니다.  

---

## Private Subnet Routing  
## 프라이빗 서브넷 라우팅  

For a server in a private subnet with both private IPv4 and IPv6 addresses, the goal is to allow internet access without permitting inbound connections from the internet.  
프라이빗 IPv4 및 IPv6 주소를 가진 프라이빗 서브넷의 서버는 인터넷 접근을 허용하면서 인터넷으로부터의 인바운드 연결을 허용하지 않는 것이 목표입니다.  

For IPv4, this is achieved by routing traffic through a NAT gateway.  
IPv4의 경우, NAT 게이트웨이를 통해 트래픽을 라우팅하여 이를 달성합니다.  

The server connects to the NAT gateway, which then connects to the internet gateway to access the internet over IPv4.  
서버는 NAT 게이트웨이에 연결되고, NAT 게이트웨이는 인터넷 게이트웨이에 연결되어 IPv4로 인터넷에 접근합니다.  

For IPv6 traffic, the server connects to an egress-only internet gateway to access the internet.  
IPv6 트래픽의 경우, 서버는 egress-only 인터넷 게이트웨이에 연결하여 인터넷에 접근합니다.  

The route table for the private subnet includes entries for local traffic, routes all IPv4 traffic (0.0.0.0/0) to the NAT gateway, and routes all IPv6 traffic (::/0) to the egress-only internet gateway.  
프라이빗 서브넷의 라우트 테이블에는 로컬 트래픽 항목, 모든 IPv4 트래픽(0.0.0.0/0)을 NAT 게이트웨이로 라우팅, 모든 IPv6 트래픽(::/0)을 egress-only 인터넷 게이트웨이로 라우팅하는 항목이 포함됩니다.  

This configuration ensures outbound IPv6 connectivity while preventing inbound IPv6 connections.  
이 구성은 아웃바운드 IPv6 연결을 보장하면서 인바운드 IPv6 연결을 차단합니다.  

---

## Summary  
## 요약  

Understanding the differences between internet gateways, NAT gateways, and egress-only internet gateways is crucial for managing IPv4 and IPv6 traffic within AWS VPCs.  
인터넷 게이트웨이, NAT 게이트웨이, egress-only 인터넷 게이트웨이의 차이를 이해하는 것은 AWS VPC 내 IPv4 및 IPv6 트래픽을 관리하는 데 매우 중요합니다.  

Internet gateways allow both inbound and outbound traffic for public subnets.  
인터넷 게이트웨이는 퍼블릭 서브넷에서 인바운드와 아웃바운드 트래픽을 모두 허용합니다.  

NAT gateways enable outbound IPv4 traffic for private subnets.  
NAT 게이트웨이는 프라이빗 서브넷에서 아웃바운드 IPv4 트래픽을 허용합니다.  

Egress-only internet gateways provide outbound IPv6 traffic for private subnets while blocking inbound connections.  
Egress-only 인터넷 게이트웨이는 프라이빗 서브넷에서 아웃바운드 IPv6 트래픽을 제공하며, 인바운드 연결은 차단합니다.  

---

## Key Takeaways  
## 핵심 요약  

- Egress-only internet gateways are used exclusively for IPv6 traffic to allow outbound connections from instances in a VPC.  
- Egress-only 인터넷 게이트웨이는 VPC 내 인스턴스의 아웃바운드 IPv6 연결을 허용하기 위해 IPv6 전용으로 사용됩니다.  

- Unlike internet gateways, egress-only internet gateways prevent the internet from initiating inbound IPv6 connections to instances.  
- 인터넷 게이트웨이와 달리, egress-only 인터넷 게이트웨이는 인터넷이 인스턴스로 인바운드 IPv6 연결을 시작하는 것을 차단합니다.  

- Route tables must be updated to direct IPv6 traffic through the egress-only internet gateway for private subnets.  
- 프라이빗 서브넷의 IPv6 트래픽을 egress-only 인터넷 게이트웨이로 라우팅하려면 라우트 테이블을 업데이트해야 합니다.  

- The distinction between internet gateways, NAT gateways, and egress-only internet gateways is essential for managing IPv4 and IPv6 traffic in AWS VPCs.  
- AWS VPC에서 IPv4 및 IPv6 트래픽을 관리하려면 인터넷 게이트웨이, NAT 게이트웨이, egress-only 인터넷 게이트웨이의 차이를 이해하는 것이 필수적입니다.  
```
