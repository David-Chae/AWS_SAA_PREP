```markdown
# Site-to-Site VPN, Virtual Private Gateway & Customer Gateway  
# 사이트 간 VPN, 가상 프라이빗 게이트웨이(VGW) 및 고객 게이트웨이(CGW)  

🎮 게임보상: "VPN Master Badge" +650 XP  

---

## Introduction to Site-to-Site VPN  
## 사이트 간 VPN 소개  

The concept of site-to-site VPN involves connecting an AWS Virtual Private Cloud (VPC) to a corporate data center using a private, encrypted connection over the public internet.  
사이트 간 VPN 개념은 AWS VPC를 기업 데이터 센터와 공용 인터넷을 통해 프라이빗하고 암호화된 연결로 연결하는 것을 의미합니다.  

This setup enables secure communication between the two networks.  
이 설정은 두 네트워크 간 안전한 통신을 가능하게 합니다.  

To establish this connection, two key components are required:  
이 연결을 설정하기 위해 두 가지 핵심 구성 요소가 필요합니다:  

- A Customer Gateway (CGW) on the corporate side.  
- 기업 측의 고객 게이트웨이(CGW)  

- A Virtual Private Gateway (VGW) on the AWS VPC side.  
- AWS VPC 측의 가상 프라이빗 게이트웨이(VGW)  

The VPN connection is encrypted and traverses the public internet, effectively linking the network of the VPC to the corporate data center's network.  
VPN 연결은 암호화되며 공용 인터넷을 통과하여 VPC 네트워크와 기업 데이터 센터 네트워크를 연결합니다.  

---

## Virtual Private Gateway (VGW)  
## 가상 프라이빗 게이트웨이(VGW)  

The VGW acts as a VPN concentrator on the AWS side of the VPN connection.  
VGW는 VPN 연결에서 AWS 측의 VPN 집중 장치 역할을 합니다.  

It is created and attached to the VPC from which the site-to-site VPN connection will be established.  
VGW는 사이트 간 VPN 연결을 설정할 VPC에 생성되어 연결됩니다.  

Additionally, it is possible to customize the Autonomous System Number (ASN) if needed.  
필요 시 자율 시스템 번호(ASN)를 사용자 지정할 수도 있습니다.  

---

## Customer Gateway (CGW)  
## 고객 게이트웨이(CGW)  

The Customer Gateway represents the physical or software device on the corporate data center side of the VPN connection.  
CGW는 VPN 연결에서 기업 데이터 센터 측의 물리적 또는 소프트웨어 장치를 나타냅니다.  

AWS maintains a list of tested and supported customer gateway devices to ensure compatibility.  
AWS는 호환성을 보장하기 위해 테스트된 지원 CGW 장치 목록을 유지합니다.  

---

## Setting Up the Customer Gateway Device  
## 고객 게이트웨이 장치 설정  

When configuring the customer gateway device, the IP address used depends on whether the device has a public or private IP:  
CGW 장치를 구성할 때 사용하는 IP 주소는 장치가 공용 IP를 갖는지 사설 IP를 갖는지에 따라 달라집니다.  

- If the CGW has a public, internet-routable IP address, this public IP is used to establish connectivity between the VGW and CGW.  
- CGW가 공용 인터넷 라우팅 가능한 IP를 갖는 경우, VGW와 CGW 간 연결을 위해 이 공용 IP를 사용합니다.  

- If the CGW has a private IP address, it is typically behind a NAT device with NAT Traversal (NAT-T) enabled.  
- CGW가 사설 IP를 갖는 경우 일반적으로 NAT 장치 뒤에 있으며 NAT-T가 활성화되어 있습니다.  

In this case, the public IP of the NAT device is used for the VPN connection.  
이 경우 VPN 연결에는 NAT 장치의 공용 IP가 사용됩니다.  

---

## Important Exam Notes  
## 시험 대비 중요 사항  

The site-to-site VPN connection will not function until route propagation is enabled in the VPC route tables for the relevant subnets.  
관련 서브넷에 대해 VPC 라우트 테이블에서 경로 전파(Route Propagation)가 활성화되어야 사이트 간 VPN 연결이 작동합니다.  

To allow ping (ICMP) traffic from on-premises to AWS EC2 instances, ensure that the ICMP protocol is enabled inbound in the security group attached to the instances.  
온프레미스에서 AWS EC2 인스턴스로 ping(ICMP) 트래픽을 허용하려면, 인스턴스에 연결된 보안 그룹에서 ICMP 인바운드가 활성화되어야 합니다.  

This is a common point of confusion in exams.  
이는 시험에서 혼동하기 쉬운 부분입니다.  

---

## AWS VPN CloudHub  
## AWS VPN CloudHub  

AWS VPN CloudHub allows multiple customer networks or data centers, each with their own customer gateway, to communicate securely through a single VPC's virtual private gateway.  
AWS VPN CloudHub는 각기 다른 CGW를 가진 여러 고객 네트워크 또는 데이터 센터가 단일 VPC의 VGW를 통해 안전하게 통신할 수 있게 합니다.  

This is achieved by establishing multiple site-to-site VPN connections to the same VGW.  
이는 동일 VGW에 대해 여러 사이트 간 VPN 연결을 설정하여 구현됩니다.  

This setup follows a low-cost hub-and-spoke model for primary or secondary network connectivity between different locations, using only VPN connections.  
이 설정은 VPN 연결만 사용하여 서로 다른 위치 간 1차 또는 2차 네트워크 연결을 위한 저비용 허브-스포크 모델을 따릅니다.  

With CloudHub, the customer networks can communicate with one another through the VPN connections established to the VGW.  
CloudHub를 통해 고객 네트워크는 VGW에 설정된 VPN 연결을 통해 서로 통신할 수 있습니다.  

Since the VPN traffic traverses the public internet, the connections are encrypted to maintain security.  
VPN 트래픽이 공용 인터넷을 통과하므로 연결은 암호화되어 보안이 유지됩니다.  

To configure CloudHub:  
CloudHub를 구성하려면:  

- Set up multiple site-to-site VPN connections on the same virtual private gateway.  
- 동일 VGW에서 여러 사이트 간 VPN 연결 설정  

- Enable dynamic routing.  
- 동적 라우팅 활성화  

- Configure route tables accordingly.  
- 라우트 테이블을 적절히 구성  

---

## Summary  
## 요약  

Site-to-site VPNs provide a secure, encrypted connection over the public internet between an AWS VPC and a corporate data center.  
사이트 간 VPN은 AWS VPC와 기업 데이터 센터 간 공용 인터넷을 통한 안전하고 암호화된 연결을 제공합니다.  

The key components are the Virtual Private Gateway on AWS and the Customer Gateway on the corporate side.  
핵심 구성 요소는 AWS 측의 VGW와 기업 측의 CGW입니다.  

Proper configuration of IP addresses, route propagation, and security group rules is essential for successful connectivity.  
성공적인 연결을 위해 IP 주소, 경로 전파(Route Propagation), 보안 그룹 규칙을 적절히 구성해야 합니다.  

AWS VPN CloudHub extends this capability to multiple customer networks, enabling secure communication across multiple sites.  
AWS VPN CloudHub는 이 기능을 여러 고객 네트워크로 확장하여 여러 사이트 간 안전한 통신을 가능하게 합니다.  

---

## Key Takeaways  
## 핵심 요약  

- Site-to-site VPN connects an AWS VPC to a corporate data center over the public internet using encrypted tunnels.  
- 사이트 간 VPN은 암호화 터널을 사용하여 AWS VPC를 기업 데이터 센터와 공용 인터넷으로 연결  

- The VPN requires a Virtual Private Gateway (VGW) on the AWS side and a Customer Gateway (CGW) device on the corporate side.  
- VPN은 AWS 측의 VGW와 기업 측 CGW 장치가 필요  

- The CGW can have a public IP or be behind a NAT device with NAT-T enabled; the public IP used depends accordingly.  
- CGW는 공용 IP를 갖거나 NAT-T가 활성화된 NAT 장치 뒤에 있을 수 있으며, VPN 연결에 사용할 공용 IP는 이에 따라 결정  

- Route propagation must be enabled in the VPC route tables for the VPN connection to function properly.  
- VPN 연결이 정상 작동하려면 VPC 라우트 테이블에서 경로 전파(Route Propagation)가 활성화되어야 함  

- AWS VPN CloudHub allows multiple customer networks to securely communicate through a single VGW using multiple VPN connections.  
- AWS VPN CloudHub는 여러 고객 네트워크가 단일 VGW를 통해 여러 VPN 연결로 안전하게 통신하도록 지원  

- Security group rules, such as enabling ICMP inbound, are necessary for certain traffic like ping to work over the VPN.  
- ping 같은 트래픽이 VPN에서 작동하려면 ICMP 인바운드 활성화 등 보안 그룹 규칙이 필요  
```
