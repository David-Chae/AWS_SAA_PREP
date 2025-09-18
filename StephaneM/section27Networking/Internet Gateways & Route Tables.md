```markdown
# Internet Gateways & Route Tables  
# 인터넷 게이트웨이와 라우트 테이블  

🎮 게임보상: "Gateway Explorer" +300 XP  

---

## Introduction to Internet Access in Subnets  
## 서브넷에서 인터넷 접근 소개  

Currently, our subnets lack internet access, and we have yet to define what constitutes a Public Subnet versus a Private Subnet.  
현재 우리 서브넷은 인터넷 접근이 없으며, 퍼블릭 서브넷과 프라이빗 서브넷이 무엇인지 아직 정의하지 않았습니다.  

To enable internet connectivity for resources within a Virtual Private Cloud (VPC), such as EC2 instances and Lambda functions, we utilize an Internet Gateway.  
EC2 인스턴스나 Lambda 함수 같은 VPC 내 리소스가 인터넷에 연결되도록 하기 위해 인터넷 게이트웨이를 사용합니다.  

---

## Internet Gateway Overview  
## 인터넷 게이트웨이 개요  

An Internet Gateway is a horizontally scalable, highly available, and redundant managed resource.  
인터넷 게이트웨이는 수평 확장이 가능하며, 고가용성과 중복성을 가진 관리형 리소스입니다.  

It must be created separately from the VPC itself.  
VPC와는 별도로 생성되어야 합니다.  

Importantly, one VPC can only be attached to a single Internet Gateway, and each Internet Gateway can only be attached to one VPC.  
중요하게도, 한 VPC는 하나의 인터넷 게이트웨이만 연결할 수 있으며, 각 인터넷 게이트웨이도 하나의 VPC에만 연결 가능합니다.  

---

## Internet Gateway Does Not Provide Internet Access Alone  
## 인터넷 게이트웨이만으로는 인터넷 접근 불가  

Internet Gateways on their own do not grant internet access.  
인터넷 게이트웨이만으로는 인터넷 접근 권한을 제공하지 않습니다.  

To enable connectivity, it is necessary to modify the Route Tables associated with the subnets.  
연결을 가능하게 하려면, 서브넷과 연결된 라우트 테이블을 수정해야 합니다.  

This configuration ensures that traffic is properly routed through the Internet Gateway to the internet.  
이 구성은 트래픽이 인터넷 게이트웨이를 통해 올바르게 라우팅되도록 보장합니다.  

---

## Configuring Internet Access for Subnets  
## 서브넷의 인터넷 접근 구성  

Consider a VPC with two subnets and one EC2 instance.  
두 개의 서브넷과 하나의 EC2 인스턴스가 있는 VPC를 생각해봅니다.  

For simplicity, other subnets are not shown in the diagram.  
단순화를 위해, 다른 서브넷은 다이어그램에 표시하지 않습니다.  

We will create an Internet Gateway within this VPC; however, this alone will not provide internet access to the subnets.  
이 VPC 내에 인터넷 게이트웨이를 생성하지만, 이것만으로는 서브넷에 인터넷 접근이 제공되지 않습니다.  

To enable internet connectivity, we must also edit the Route Tables.  
인터넷 연결을 가능하게 하려면 라우트 테이블도 수정해야 합니다.  

Specifically, we will create a Public EC2 instance in the Public Subnet and configure the Route Table so that the EC2 instance can route traffic through the router to the Internet Gateway, which then connects to the internet.  
구체적으로, 퍼블릭 서브넷에 퍼블릭 EC2 인스턴스를 만들고 라우트 테이블을 구성하여, EC2 인스턴스의 트래픽이 라우터를 통해 인터넷 게이트웨이로 라우팅되어 인터넷에 연결되도록 합니다.  

---

## Next Steps  
## 다음 단계  

In the following lecture, we will explore the detailed steps to configure the Internet Gateway and Route Tables to enable internet access for our subnets.  
다음 강의에서는 서브넷에서 인터넷 접근을 가능하게 하기 위해 인터넷 게이트웨이와 라우트 테이블을 구성하는 상세 단계를 살펴보겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- An Internet Gateway enables resources within a VPC to connect to the internet.  
- 인터넷 게이트웨이는 VPC 내 리소스가 인터넷에 연결되도록 합니다.  

- Internet Gateways are horizontally scalable, highly available, and redundant managed resources.  
- 인터넷 게이트웨이는 수평 확장 가능하며, 고가용성과 중복성을 가진 관리형 리소스입니다.  

- Each VPC can be attached to only one Internet Gateway, and vice versa.  
- 각 VPC는 하나의 인터넷 게이트웨이에만 연결 가능하며, 인터넷 게이트웨이도 하나의 VPC에만 연결됩니다.  

- Internet access requires both an Internet Gateway and appropriate Route Table configurations.  
- 인터넷 접근을 위해서는 인터넷 게이트웨이와 적절한 라우트 테이블 구성이 모두 필요합니다.  
```

🎮 게임보상 완료: "Gateway Explorer" +300 XP 🏆
