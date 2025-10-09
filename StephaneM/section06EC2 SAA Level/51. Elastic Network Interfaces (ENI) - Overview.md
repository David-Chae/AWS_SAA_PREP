# Elastic Network Interfaces (ENI) - Overview  
# 탄력적 네트워크 인터페이스 (ENI) - 개요  
→ ENI는 AWS VPC 안에서 네트워크 연결을 제공하는 가상 네트워크 카드 역할을 함.  

---

## Introduction to Elastic Network Interfaces (ENI)  
## 탄력적 네트워크 인터페이스 (ENI) 소개  
→ ENI는 VPC 안의 논리적 구성요소로, 네트워크 연결을 담당하는 가상 네트워크 카드임.  

Elastic Network Interfaces, abbreviated as ENI, are logical components within a Virtual Private Cloud (VPC).  
탄력적 네트워크 인터페이스(ENI)는 가상 사설 클라우드(VPC) 안의 논리적 구성 요소임.  
→ ENI는 VPC 내에서 가상의 네트워크 연결 포인트로 작동.  

They represent virtual network cards that provide network connectivity to EC2 instances and other resources.  
이들은 EC2 인스턴스 및 다른 리소스에 네트워크 연결을 제공하는 가상 네트워크 카드 역할을 함.  
→ 마치 물리적 랜카드처럼 동작하지만 가상화된 네트워크 장치임.  

ENIs are essential because they grant EC2 instances access to the network.  
ENI는 EC2 인스턴스가 네트워크에 접근할 수 있게 해주므로 필수적임.  
→ ENI 없이는 인스턴스가 네트워크와 통신 불가.  

However, their use is not limited to EC2 instances, as we will explore later in this course.  
하지만 ENI는 EC2 인스턴스에만 한정되지 않으며, 이후에 다른 활용법도 다룰 예정임.  
→ ENI는 EC2 외에도 다양한 AWS 네트워크 리소스에서 사용 가능.  

---

## ENI Attachment to EC2 Instances  
## ENI와 EC2 인스턴스 연결  
→ ENI는 EC2 인스턴스에 붙어 네트워크 연결을 제공.  

Consider an Availability Zone with a single EC2 instance.  
하나의 가용 영역에 단일 EC2 인스턴스가 있다고 가정해보자.  
→ 예시를 통해 ENI가 어떻게 작동하는지 설명.  

Attached to this instance is the primary ENI, typically named eth0.  
이 인스턴스에는 기본 ENI가 연결되며, 보통 eth0이라 불림.  
→ eth0은 EC2 인스턴스의 첫 번째 네트워크 카드임.  

This primary ENI provides the EC2 instance with network connectivity, including a private IP address.  
이 기본 ENI는 EC2 인스턴스에 네트워크 연결을 제공하며, 여기에는 사설 IP 주소가 포함됨.  
→ ENI를 통해 인스턴스는 네트워크에서 통신 가능.  

Each ENI can have the following attributes:  
각 ENI는 다음과 같은 속성을 가짐:  
→ ENI는 여러 네트워크 속성을 동시에 가짐.  

- A primary private IPv4 address.  
- 기본 사설 IPv4 주소  
→ 인스턴스가 네트워크에서 식별되는 주요 주소.  

- One or more secondary IPv4 addresses.  
- 하나 이상의 보조 IPv4 주소  
→ 여러 IP를 할당할 수 있어 유연한 네트워크 구성 가능.  

For example, an instance may have a secondary ENI attached as eth1, which provides an additional private IPv4 address.  
예를 들어, 인스턴스에 eth1이라는 보조 ENI가 붙어 추가적인 사설 IPv4 주소를 제공할 수 있음.  
→ 다중 네트워크 인터페이스를 통한 확장성 제공.  

---

## IP Addressing and Security Groups  
## IP 주소와 보안 그룹  
→ ENI는 IP 주소뿐만 아니라 보안 그룹도 연결할 수 있음.  

Each ENI can also have an elastic IPv4 address associated with its private IPv4 address, or one or more public IPv4 addresses.  
각 ENI는 사설 IPv4 주소와 연계된 탄력적 IPv4 주소 또는 하나 이상의 공용 IPv4 주소를 가질 수 있음.  
→ ENI는 사설·공용 IP를 동시에 지원.  

This setup allows the ENI to have both private and public IP addresses, as will be demonstrated in the hands-on section.  
이 설정은 ENI가 사설 및 공용 IP 주소를 동시에 갖게 해줌. 실습에서 이를 확인할 수 있음.  
→ 프라이빗+퍼블릭 접근을 동시에 제공 가능.  

Additionally, one or more security groups can be attached to each ENI, controlling inbound and outbound traffic.  
또한, 각 ENI에는 하나 이상의 보안 그룹을 연결할 수 있어 인바운드 및 아웃바운드 트래픽을 제어함.  
→ ENI 단위로 보안 제어가 가능.  

Other attributes of ENIs include a MAC address and additional properties, but the primary focus here is on the most important aspects relevant to network connectivity.  
ENI의 다른 속성으로는 MAC 주소 등이 있지만, 여기서는 네트워크 연결과 관련된 핵심 요소에만 집중함.  
→ ENI는 물리적 네트워크 카드처럼 MAC 주소도 가짐.  

---

## ENI Independence and Mobility  
## ENI의 독립성과 이동성  
→ ENI는 인스턴스와 독립적으로 생성되고 이동 가능.  

ENIs can be created independently from EC2 instances.  
ENI는 EC2 인스턴스와 독립적으로 생성될 수 있음.  
→ 반드시 인스턴스 생성 시 만들어지는 것은 아님.  

They can be attached to instances on the fly or moved between instances to facilitate failover scenarios.  
이들은 필요할 때 인스턴스에 붙이거나 다른 인스턴스로 옮겨 장애 조치(failover)를 쉽게 할 수 있음.  
→ ENI를 이동시켜 서비스 연속성 확보 가능.  

It is important to note that ENIs are bound to a specific Availability Zone (AZ).  
중요한 점은 ENI는 특정 가용 영역(AZ)에 묶여 있다는 것임.  
→ 다른 AZ의 인스턴스에는 붙일 수 없음.  

This means that an ENI created in a particular AZ can only be attached to instances within that same AZ.  
즉, 특정 AZ에서 생성된 ENI는 해당 AZ 안의 인스턴스에만 연결 가능함.  
→ ENI의 영역 제한성을 이해해야 함.  

---

## Example of ENI Movement Between Instances  
## ENI 이동 예시  
→ 동일 AZ 내에서 ENI를 다른 인스턴스로 옮길 수 있음.  

Consider two EC2 instances within the same Availability Zone.  
같은 가용 영역 내에 두 개의 EC2 인스턴스가 있다고 가정해보자.  

The first instance has a secondary ENI attached as eth1.  
첫 번째 인스턴스에는 eth1이라는 보조 ENI가 붙어 있음.  

This ENI can be detached from the first instance and attached to the second instance, effectively moving the private IP address from the first to the second instance.  
이 ENI를 첫 번째 인스턴스에서 분리해 두 번째 인스턴스에 붙이면, 사설 IP가 첫 번째에서 두 번째 인스턴스로 이동하게 됨.  
→ IP 주소를 그대로 유지하면서 서비스 이전 가능.  

This capability is particularly useful for failover purposes.  
이 기능은 장애 조치(failover) 상황에서 특히 유용함.  

For example, if an EC2 instance is accessed via a private static IP, moving the ENI to another instance allows the IP to follow the failover instance seamlessly.  
예를 들어, 사설 고정 IP로 EC2 인스턴스에 접근 중일 때, ENI를 다른 인스턴스로 옮기면 해당 IP가 장애 조치 인스턴스로 그대로 따라감.  
→ IP 이동 덕분에 서비스 중단 최소화 가능.  

---

## Hands-On Demonstration  
## 실습 시연  
→ ENI의 실제 동작을 직접 확인.  

We will now proceed to a hands-on demonstration to observe what ENIs look like and how they function in practice.  
이제 실습을 통해 ENI가 어떤 모습이며 실제로 어떻게 동작하는지 확인할 것임.  

---

## Key Takeaways  
## 핵심 요약  
→ ENI의 핵심 특징을 다시 정리.  

- Elastic Network Interfaces (ENIs) are virtual network cards within a VPC that provide network connectivity to EC2 instances.  
- ENI는 VPC 내의 가상 네트워크 카드로, EC2 인스턴스에 네트워크 연결을 제공함.  

- Each ENI can have a primary private IPv4 address, multiple secondary IPv4 addresses, and associated elastic or public IPv4 addresses.  
- 각 ENI는 기본 사설 IPv4, 여러 보조 IPv4, 탄력적 또는 공용 IPv4 주소를 가질 수 있음.  

- ENIs can be created independently of EC2 instances and attached or moved between instances within the same Availability Zone for failover.  
- ENI는 EC2와 독립적으로 생성 가능하며, 같은 AZ 내에서 인스턴스 간 이동해 장애 조치에 활용 가능함.  

- ENIs are bound to a specific Availability Zone and support multiple security groups and MAC addresses.  
- ENI는 특정 AZ에 묶이며, 다수의 보안 그룹과 MAC 주소를 지원함.  
