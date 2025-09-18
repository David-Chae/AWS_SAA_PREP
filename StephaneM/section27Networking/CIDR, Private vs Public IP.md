```markdown
# CIDR, Private vs Public IP  
# CIDR, 사설 IP와 공인 IP  

🎮 게임보상: "Network Novice" +300 XP  

---

## Introduction to CIDR  
## CIDR 소개  

Classless Inter-Domain Routing, abbreviated as CIDR, is a method for allocating IP addresses.  
CIDR(Classless Inter-Domain Routing, 무클래스 도메인 라우팅)은 IP 주소를 할당하는 방법입니다.  

Throughout this course, we will refer to it simply as CIDR.  
이 강좌에서는 단순히 CIDR이라고 부르겠습니다.  

We have encountered CIDR before, especially when examining security group rules in AWS.  
우리는 이전에 특히 AWS에서 보안 그룹 규칙을 확인할 때 CIDR을 접했습니다.  

For example, in security group rules, the source column often contains an IP address followed by a slash and a number, which is our first introduction to CIDRs.  
예를 들어, 보안 그룹 규칙에서 "source" 열에는 종종 IP 주소 뒤에 슬래시(/)와 숫자가 붙어 있는데, 이것이 CIDR의 첫 번째 소개입니다.  

---

CIDRs help define IP address ranges.  
CIDR은 IP 주소 범위를 정의하는 데 도움을 줍니다.  

For instance, an IP address with a /32 suffix represents only one IP address.  
예를 들어, /32 접미사가 붙은 IP 주소는 단 하나의 IP를 의미합니다.  

Conversely, 0.0.0.0/0 represents all IP addresses.  
반대로, 0.0.0.0/0은 모든 IP 주소를 의미합니다.  

There are many possibilities in between these extremes.  
이 극단 사이에는 다양한 범위가 가능합니다.  

For example, 192.168.0.0/26 represents a range of 64 IP addresses, as illustrated in the following slide.  
예를 들어, 192.168.0.0/26은 64개의 IP 주소 범위를 나타냅니다.  

---

## How CIDR Works  
## CIDR 작동 원리  

CIDR consists of two components:  
CIDR은 두 가지 구성 요소로 이루어져 있습니다:  

- Base IP: This is an IP address contained within the range, usually the beginning of the range but not necessarily. Examples include 10.0.0.0 or 192.168.0.0.  
- 기본 IP: 범위 내에 포함된 IP 주소로, 일반적으로 범위의 시작점이지만 반드시 시작점일 필요는 없습니다. 예: 10.0.0.0, 192.168.0.0  

- Subnet Mask: This defines how many bits can change in the IP address. The subnet mask is denoted by a slash followed by a number, such as /0, /24, or /32.  
- 서브넷 마스크: IP 주소에서 변경 가능한 비트 수를 정의합니다. 슬래시 뒤에 숫자로 표시됩니다. 예: /0, /24, /32  

---

The subnet mask can take two forms. For example:  
서브넷 마스크는 두 가지 형태로 나타낼 수 있습니다. 예:  

- /8 is equivalent to a subnet mask of 255.0.0.0  
- /8은 255.0.0.0 서브넷 마스크와 동일합니다.  

- /16 is equivalent to 255.255.0.0  
- /16은 255.255.0.0과 동일합니다.  

However, the most common form used in this course and in AWS is the slash notation (e.g., /8, /16).  
하지만 이 강좌와 AWS에서 가장 일반적으로 사용하는 형태는 슬래시 표기법입니다.  

---

## Detailed Look at Subnet Masks  
## 서브넷 마스크 상세  

The subnet mask defines which values can change from the base IP.  
서브넷 마스크는 기본 IP에서 변경 가능한 값을 정의합니다.  

For example:  
예를 들어:  

- An IP address with /32 allows for only one IP address, calculated as 2^0.  
- /32는 단 하나의 IP만 허용합니다. 계산식: 2^0  

- /31 allows for two IP addresses, such as 192.168.0.0 and 192.168.0.1.  
- /31은 두 개의 IP를 허용합니다. 예: 192.168.0.0, 192.168.0.1  

- /30 allows for 4 IP addresses, ranging from .0 to .3.  
- /30은 4개의 IP를 허용합니다. 범위: .0 ~ .3  

- /29 allows for 8 IP addresses, from .0 to .7.  
- /29는 8개의 IP를 허용합니다. 범위: .0 ~ .7  

- /28 allows for 16 IP addresses, from .0 to .15.  
- /28은 16개의 IP를 허용합니다. 범위: .0 ~ .15  

This pattern continues exponentially, as shown in the table below:  
아래 표와 같이 지수적으로 증가합니다:  

| Subnet Mask | Number of IPs | IP Range Example |  
|-------------|---------------|-----------------|  
| /24         | 256           | .0 to .255      |  
| /16         | 65,536        | 마지막 두 옥텟 변경 |  
| /0          | All IPs       | 전체 IPv4 공간 |  

---

Remember, an IP address consists of 4 octets.  
IP 주소는 4개의 옥텟으로 구성되어 있습니다.  

The subnet mask determines how many of these octets can vary:  
서브넷 마스크는 몇 개의 옥텟이 변경될 수 있는지 결정합니다.  

- /32 means no octets can change.  
- /32: 옥텟 변경 불가  

- /24 means the last octet can change.  
- /24: 마지막 옥텟 변경 가능  

- /16 means the last two octets can change.  
- /16: 마지막 두 옥텟 변경 가능  

- /8 means the last three octets can change.  
- /8: 마지막 세 옥텟 변경 가능  

- /0 means all octets can change.  
- /0: 모든 옥텟 변경 가능  

---

## Exercise: Understanding CIDR Notation  
## 연습문제: CIDR 표기법 이해  

Let's apply what we've learned with a few examples:  
배운 내용을 몇 가지 예제로 적용해 봅시다:  

- 192.168.0.0/24: The /24 means the last octet can change, so there are 256 IP addresses ranging from 192.168.0.0 to 192.168.0.255.  
- 192.168.0.0/24: /24는 마지막 옥텟이 변경 가능하다는 의미이며, 192.168.0.0 ~ 192.168.0.255까지 256개의 IP가 포함됩니다.  

- 192.168.0.0/16: The /16 means the last two octets can change, resulting in 65,536 IP addresses.  
- 192.168.0.0/16: /16은 마지막 두 옥텟이 변경 가능하며, 65,536개의 IP가 생성됩니다.  

- 134.56.78.123/32: The /32 means only one IP address, so just 134.56.78.123.  
- 134.56.78.123/32: /32는 단 하나의 IP만 포함하므로, 134.56.78.123 하나입니다.  

- 0.0.0.0/0: This represents the entire IPv4 address space.  
- 0.0.0.0/0: 전체 IPv4 주소 공간을 의미합니다.  

---

If you need assistance calculating IP ranges or CIDRs, there are handy websites available that can convert CIDR notation to IP ranges and vice versa.  
IP 범위 또는 CIDR 계산이 필요할 경우, CIDR 표기법을 IP 범위로 변환하거나 반대로 변환해주는 유용한 웹사이트가 있습니다.  

---

## Using Online Tools for CIDR Calculations  
## CIDR 계산용 온라인 도구 사용  

For example, entering 10.0.0.0/16 into such a tool will display the first and last IP addresses in the range, the total number of IPs included, and other useful information.  
예를 들어, 10.0.0.0/16을 입력하면 범위 내 첫 번째와 마지막 IP, 포함된 총 IP 수, 기타 유용한 정보를 표시합니다.  

Similarly, entering an IP range can help determine the corresponding CIDR notation.  
마찬가지로, IP 범위를 입력하면 해당 범위에 대응하는 CIDR 표기법을 알 수 있습니다.  

These tools are very helpful when working with networking.  
이 도구들은 네트워킹 작업 시 매우 유용합니다.  

---

## Public vs Private IP Addresses  
## 공인 IP와 사설 IP  

The Internet Assigned Numbers Authority (IANA) has designated certain blocks of IPv4 addresses for private LAN networks, which are local networks, and others for public internet addresses.  
IANA(인터넷 번호 관리 기관)는 특정 IPv4 블록을 사설 LAN 네트워크용과 공인 인터넷 주소용으로 지정했습니다.  

---

The private IP address ranges include:  
사설 IP 범위는 다음과 같습니다:  

- 10.0.0.0/8: A large private IP range commonly used in big networks.  
- 10.0.0.0/8: 대규모 네트워크에서 흔히 사용되는 넓은 사설 IP 범위  

- 172.16.0.0/12: Another private IP range.  
- 172.16.0.0/12: 또 다른 사설 IP 범위  

- 192.168.0.0/16: Typically used for home networks; devices connected to a home router often have IPs starting with 192.  
- 192.168.0.0/16: 주로 가정용 네트워크에서 사용; 홈 라우터에 연결된 장치는 192로 시작하는 IP를 갖습니다.  

All other IP addresses outside these ranges are public IP addresses used on the internet.  
이 범위 밖의 모든 IP는 인터넷에서 사용되는 공인 IP입니다.  

---

## Summary  
## 요약  

These are the basics of IPv4 addressing and CIDR notation.  
이것이 IPv4 주소와 CIDR 표기법의 기본 개념입니다.  

Understanding these concepts is essential for networking and configuring security groups in cloud environments like AWS.  
이 개념을 이해하는 것은 AWS와 같은 클라우드 환경에서 네트워킹과 보안 그룹 구성에 필수적입니다.  

I hope this lecture has been helpful, and I look forward to seeing you in the next lecture.  
이 강의가 도움이 되었기를 바라며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- CIDR (Classless Inter-Domain Routing) is a method for allocating IP addresses using a base IP and subnet mask.  
- CIDR은 기본 IP와 서브넷 마스크를 사용하여 IP 주소를 할당하는 방법입니다.  

- The subnet mask, denoted by /n, defines how many bits can change in the IP address, determining the size of the IP range.  
- 서
```


브넷 마스크(/n)는 IP에서 변경 가능한 비트 수를 정의하며, IP 범위 크기를 결정합니다.

* Private IP address ranges are reserved for local networks and include 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16.

* 사설 IP 범위는 로컬 네트워크용으로 예약되어 있으며, 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16이 포함됩니다.

* Public IP addresses are all other IPs outside the private ranges and are used on the internet.

* 공인 IP는 사설 범위 외의 모든 IP이며, 인터넷에서 사용됩니다.

```

🎮 게임보상 완료: "Network Novice" +300 XP 🏆  
