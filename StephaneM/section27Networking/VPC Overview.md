```markdown
# VPC Overview  
# VPC 개요  

🎮 게임보상: "VPC Builder" +300 XP  

---

## Introduction to VPC  
## VPC 소개  

Let's begin by creating our first Virtual Private Cloud (VPC) in AWS.  
AWS에서 첫 번째 Virtual Private Cloud(VPC)를 만들어보겠습니다.  

A VPC stands for Virtual Private Cloud.  
VPC는 Virtual Private Cloud의 약자입니다.  

You can have multiple VPCs within a single AWS region.  
하나의 AWS 리전 내에서 여러 VPC를 생성할 수 있습니다.  

The default maximum is five VPCs per region; however, this is a soft limit and can be increased upon request.  
기본 제한은 리전당 5개의 VPC지만, 이는 소프트 리미트로 요청 시 늘릴 수 있습니다.  

---

Each VPC can be assigned up to five CIDR blocks.  
각 VPC에는 최대 5개의 CIDR 블록을 할당할 수 있습니다.  

The size of each CIDR block must be between a minimum of /28 and a maximum of /16.  
각 CIDR 블록의 크기는 최소 /28, 최대 /16 사이여야 합니다.  

A /28 CIDR block corresponds to at least 16 IP addresses, while a /16 CIDR block corresponds to a maximum of 65,536 IP addresses.  
/28 CIDR 블록은 최소 16개의 IP 주소를 의미하며, /16 CIDR 블록은 최대 65,536개의 IP 주소를 의미합니다.  

---

Since a VPC is a private resource, only private IPv4 address ranges are allowed.  
VPC는 사설 리소스이므로 사설 IPv4 주소 범위만 사용할 수 있습니다.  

The private IPv4 ranges include:  
사설 IPv4 주소 범위는 다음과 같습니다.  

- 10.0.0.0/8  
- 172.16.0.0/12  
- 192.168.0.0/16  

---

## Choosing CIDR Ranges for Your VPC  
## VPC를 위한 CIDR 범위 선택  

When selecting the CIDR range for your VPC, you can assign any private IP range you prefer.  
VPC의 CIDR 범위를 선택할 때 원하는 사설 IP 범위를 할당할 수 있습니다.  

However, it is crucial to ensure that your VPC's CIDR block does not overlap with other VPCs, networks, or corporate networks you may connect to in the future.  
하지만 VPC의 CIDR 블록이 다른 VPC, 네트워크 또는 향후 연결할 수 있는 회사 네트워크와 겹치지 않도록 하는 것이 중요합니다.  

The reason for avoiding overlapping CIDR ranges is to enable seamless connectivity between networks.  
CIDR 범위가 겹치지 않아야 하는 이유는 네트워크 간 원활한 연결을 가능하게 하기 위함입니다.  

Overlapping IP address ranges can cause routing conflicts and connectivity issues.  
IP 주소 범위가 겹치면 라우팅 충돌과 연결 문제를 발생시킬 수 있습니다.  

---

## Summary  
## 요약  

By the end of this hands-on session, we will have created a simple VPC within an AWS region.  
이번 실습이 끝나면 AWS 리전 내에서 간단한 VPC를 생성하게 됩니다.  

Let's get started.  
시작해봅시다.  

---

## Key Takeaways  
## 핵심 요약  

- A Virtual Private Cloud (VPC) is a private network resource within AWS.  
- VPC는 AWS 내의 사설 네트워크 리소스입니다.  

- You can create multiple VPCs per AWS region, with a default soft limit of five.  
- AWS 리전당 여러 개의 VPC를 생성할 수 있으며, 기본 소프트 제한은 5개입니다.  

- Each VPC can have up to five CIDR blocks, with sizes ranging from /28 (16 IPs) to /16 (65,536 IPs).  
- 각 VPC는 최대 5개의 CIDR 블록을 가질 수 있으며, 크기는 /28(16 IP)부터 /16(65,536 IP)까지 가능합니다.  

- Only private IPv4 address ranges are allowed for VPCs.  
- VPC에는 사설 IPv4 주소 범위만 허용됩니다.  

- It is important to avoid overlapping CIDR ranges between VPCs and other networks to enable connectivity.  
- VPC와 다른 네트워크 간 CIDR 범위가 겹치지 않도록 하는 것이 연결을 위해 중요합니다.  
```

🎮 게임보상 완료: "VPC Builder" +300 XP 🏆
