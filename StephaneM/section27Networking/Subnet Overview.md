```markdown
# Subnet Overview  
# 서브넷 개요  

🎮 게임보상: "Subnet Explorer" +300 XP  

---

## Introduction to Subnets in a VPC  
## VPC 내 서브넷 소개  

The next step is to add subnets into our Virtual Private Cloud (VPC).  
다음 단계는 Virtual Private Cloud(VPC)에 서브넷을 추가하는 것입니다.  

We will create two subnets: one public subnet and one private subnet.  
우리는 두 개의 서브넷을 만들 것입니다: 하나는 퍼블릭 서브넷, 하나는 프라이빗 서브넷입니다.  

Both subnets will be within a single availability zone.  
두 서브넷 모두 단일 가용 영역(Availability Zone) 내에 위치합니다.  

We will also explore what makes a subnet public or private.  
또한 서브넷이 퍼블릭 또는 프라이빗이 되는 조건도 알아볼 것입니다.  

---

## What is a Subnet?  
## 서브넷이란 무엇인가?  

A subnet is a sub-range of IPv4 addresses within your VPC.  
서브넷은 VPC 내 IPv4 주소의 하위 범위입니다.  

AWS reserves five IP addresses in each subnet.  
AWS는 각 서브넷에서 다섯 개의 IP 주소를 예약합니다.  

Specifically, the first four IP addresses and the last one are reserved.  
구체적으로 말하면 처음 네 개의 IP와 마지막 하나가 예약됩니다.  

These reserved IP addresses are not available for use and cannot be assigned to an EC2 instance.  
이 예약된 IP 주소들은 사용 불가하며 EC2 인스턴스에 할당할 수 없습니다.  

For example, if you have a CIDR block of 10.0.0.0/24, there are several reserved IP addresses:  
예를 들어, CIDR 블록이 10.0.0.0/24라면 다음과 같은 예약 IP가 있습니다:  

- The first IP address, which is the network address.  
- 첫 번째 IP 주소는 네트워크 주소입니다.  

- The second IP address (.1), reserved by AWS for the VPC router.  
- 두 번째 IP(.1)는 VPC 라우터용으로 AWS가 예약합니다.  

- The third IP address (.2), reserved by AWS for mapping to Amazon provided DNS.  
- 세 번째 IP(.2)는 AWS 제공 DNS 매핑용으로 예약됩니다.  

- The fourth IP address (.3), which is currently not used but reserved for future use.  
- 네 번째 IP(.3)는 현재 사용되지 않지만 미래 사용을 위해 예약됩니다.  

- The last IP address (.255), which is the network broadcast address.  
- 마지막 IP(.255)는 네트워크 브로드캐스트 주소입니다.  

Since AWS does not support broadcast in a VPC, this last address is reserved and cannot be used.  
AWS는 VPC에서 브로드캐스트를 지원하지 않으므로, 마지막 주소는 예약되어 사용 불가입니다.  

---

## Exam Tip: Choosing Subnet Size  
## 시험 팁: 서브넷 크기 선택  

If you need 29 IP addresses in a subnet for EC2 instances, you cannot choose a subnet with a /27 mask.  
EC2 인스턴스용으로 29개의 IP가 필요하다면 /27 서브넷을 선택할 수 없습니다.  

A /27 subnet contains 32 IP addresses, but after removing the five reserved IP addresses, only 27 usable IP addresses remain, which is less than the 29 needed.  
/27 서브넷은 32개의 IP 주소를 가지지만, 예약된 다섯 개를 제외하면 27개만 사용 가능하여 필요한 29개보다 적습니다.  

Instead, you should choose a subnet size of /26, which provides 64 IP addresses.  
대신 /26 서브넷을 선택해야 하며, 이 경우 64개의 IP 주소를 제공합니다.  

After subtracting the five reserved IP addresses, you have 59 usable IP addresses, which is greater than the 29 required.  
예약된 5개의 IP를 제외하면 59개의 사용 가능한 IP가 남아, 필요한 29개보다 많습니다.  

In the next lecture, we will proceed to create our first subnets.  
다음 강의에서는 첫 번째 서브넷을 생성할 예정입니다.  

---

## Key Takeaways  
## 핵심 요약  

- A subnet is a sub-range of IPv4 addresses within a VPC.  
- 서브넷은 VPC 내 IPv4 주소의 하위 범위입니다.  

- AWS reserves five IP addresses in each subnet: the first four and the last one.  
- AWS는 각 서브넷에서 5개의 IP 주소를 예약합니다: 처음 네 개와 마지막 하나.  

- Reserved IP addresses include network address, VPC router, Amazon DNS, future use, and broadcast address.  
- 예약 IP에는 네트워크 주소, VPC 라우터, AWS DNS, 미래 사용, 브로드캐스트 주소가 포함됩니다.  

- When selecting subnet size, account for reserved IPs to ensure enough usable addresses for EC2 instances.  
- 서브넷 크기 선택 시 예약 IP를 고려하여 EC2 인스턴스용 충분한 사용 가능 IP가 있는지 확인해야 합니다.  
```

🎮 게임보상 완료: "Subnet Explorer" +300 XP 🏆
