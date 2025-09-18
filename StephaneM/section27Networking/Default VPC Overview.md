```markdown
# Default VPC Overview  
# 기본 VPC 개요  

🎮 게임보상: "VPC Explorer" +300 XP  

---

## Default VPC Overview  
## 기본 VPC 개요  

In this lecture, we will perform a quick walkthrough of the Virtual Private Cloud (VPC) that is created with your AWS account, known as the default VPC.  
이번 강의에서는 AWS 계정 생성 시 기본적으로 생성되는 Virtual Private Cloud(VPC), 즉 기본 VPC를 빠르게 살펴보겠습니다.  

All new AWS accounts have a default VPC so that you can start using it right away.  
모든 새로운 AWS 계정에는 기본 VPC가 있어 즉시 사용할 수 있습니다.  

New EC2 instances launched into the default VPC, if you do not specify any subnets, will be placed there by default.  
서브넷을 지정하지 않고 기본 VPC에 새로운 EC2 인스턴스를 시작하면 자동으로 기본 VPC에 배치됩니다.  

When you start with your account, you only have one VPC, which is the default VPC.  
계정 시작 시 하나의 VPC만 존재하며, 그것이 바로 기본 VPC입니다.  

---

The default VPC has internet connectivity by default.  
기본 VPC는 기본적으로 인터넷 연결을 제공합니다.  

This is why our instances are able to access the internet immediately.  
이 때문에 인스턴스가 생성 직후 바로 인터넷에 접속할 수 있습니다.  

Each EC2 instance within the default VPC receives a public IPv4 address, which enables us to connect to our EC2 instances right away after creation.  
기본 VPC 내의 각 EC2 인스턴스는 공인 IPv4 주소를 받아 생성 직후 바로 접속할 수 있습니다.  

Additionally, each instance gets both a public and a private IPv4 DNS name.  
또한, 각 인스턴스는 공인 및 사설 IPv4 DNS 이름을 함께 받습니다.  

---

Let's now go into the AWS Management Console to examine this default VPC.  
이제 AWS Management Console에서 기본 VPC를 확인해 보겠습니다.  

We will navigate to the VPC service.  
VPC 서비스로 이동합니다.  

The reason for having a default VPC is to simplify the initial experience for newcomers to the cloud.  
기본 VPC가 존재하는 이유는 클라우드 초보자들이 시작할 때 경험을 단순화하기 위해서입니다.  

Without a default VPC, it would be very complicated for new users to start using AWS.  
기본 VPC가 없으면 신규 사용자가 AWS를 시작하기 매우 복잡합니다.  

---

However, it is best practice, especially if you have networking knowledge, to create your own VPCs in production accounts instead of using the default VPC.  
하지만 특히 네트워킹 지식이 있다면 운영 계정에서는 기본 VPC 대신 자체 VPC를 생성하는 것이 모범 사례입니다.  

---

On the VPC dashboard, on the left-hand side, you will find your VPCs.  
VPC 대시보드 왼쪽에서 VPC 목록을 확인할 수 있습니다.  

Currently, one VPC is created by default.  
현재 기본적으로 하나의 VPC가 생성되어 있습니다.  

It does not have a custom name but is labeled as the default VPC because it is created automatically.  
사용자 정의 이름은 없지만 자동 생성되므로 기본 VPC로 표시됩니다.  

This VPC has an IPv4 CIDR block defined.  
이 VPC에는 IPv4 CIDR 블록이 정의되어 있습니다.  

Using an IP range calculator, we can determine the range of IP addresses in this CIDR block.  
IP 범위 계산기를 사용하면 CIDR 블록 내 IP 범위를 확인할 수 있습니다.  

The CIDR is a /16, which means the last two octets of the IP address can vary.  
CIDR은 /16으로, 마지막 두 옥텟이 변경될 수 있음을 의미합니다.  

This results in a total of 65,536 possible IP addresses in that range.  
이 범위에는 총 65,536개의 IP 주소가 가능합니다.  

---

Currently, only one IPv4 CIDR block is associated with the VPC.  
현재 VPC에는 하나의 IPv4 CIDR 블록만 연결되어 있습니다.  

There are no IPv6 CIDRs, flow logs are not enabled, and there are no tags associated with the VPC.  
IPv6 CIDR는 없고, 플로우 로그도 활성화되지 않았으며, 태그도 연결되어 있지 않습니다.  

---

Exploring the menu options, we see the main route table, main network ACLs, and other components.  
메뉴 옵션을 살펴보면 기본 라우트 테이블, 기본 네트워크 ACL, 기타 구성 요소가 있습니다.  

We will examine these in detail later in the course, one at a time.  
이 요소들은 강좌 후반부에서 하나씩 자세히 살펴볼 예정입니다.  

For now, let's explore the menu.  
우선 메뉴를 살펴봅시다.  

---

There are three subnets already created and linked to the default VPC.  
기본 VPC에는 이미 세 개의 서브넷이 생성되어 연결되어 있습니다.  

Each subnet has its own IPv4 CIDR block.  
각 서브넷은 자체 IPv4 CIDR 블록을 가지고 있습니다.  

On the right-hand side, you can see the availability zones; each subnet is in a different availability zone.  
오른쪽에서 가용 영역을 확인할 수 있으며, 각 서브넷은 서로 다른 가용 영역에 위치합니다.  

This design provides a highly available architecture by default.  
이 설계는 기본적으로 고가용성을 제공합니다.  

---

For example, examining one subnet, we can calculate its CIDR range.  
예를 들어, 하나의 서브넷을 살펴보면 CIDR 범위를 계산할 수 있습니다.  

This subnet has a total of 4,096 hosts.  
이 서브넷에는 총 4,096개의 호스트가 있습니다.  

However, in the subnets console, the number of available IPv4 addresses is 4,091.  
하지만 서브넷 콘솔에서는 사용 가능한 IPv4 주소가 4,091개로 표시됩니다.  

We will explore why five IP addresses are reserved later in the course.  
5개의 IP가 예약된 이유는 강좌 후반부에서 다룰 예정입니다.  

The available IP count would be lower if the subnet is already in use.  
서브넷이 이미 사용 중이면 사용 가능한 IP 수는 더 적어집니다.  

---

Each subnet has an associated route table and network ACL.  
각 서브넷은 라우트 테이블과 네트워크 ACL을 갖고 있습니다.  

The default subnets have the setting "auto-assign public IPv4 address" enabled.  
기본 서브넷은 "공인 IPv4 주소 자동 할당" 설정이 활성화되어 있습니다.  

This means any EC2 instance created in these subnets will automatically receive a public IPv4 address.  
즉, 해당 서브넷에서 생성된 모든 EC2 인스턴스는 자동으로 공인 IPv4 주소를 받습니다.  

---

Flow logs are not enabled for the subnets.  
서브넷에 대한 플로우 로그는 활성화되어 있지 않습니다.  

The route table exists and will be examined shortly.  
라우트 테이블은 존재하며 곧 자세히 살펴볼 예정입니다.  

The network ACL allows all traffic on all protocols from everywhere for both inbound and outbound directions.  
네트워크 ACL은 모든 프로토콜에 대해 모든 트래픽을 인바운드 및 아웃바운드에서 허용합니다.  

This configuration ensures that any instance launched into these subnets will have network connectivity.  
이 구성은 서브넷 내에서 생성되는 모든 인스턴스가 네트워크에 연결될 수 있도록 합니다.  

---

There are no CIDR reservations or tags for the subnets.  
서브넷에는 CIDR 예약이나 태그가 없습니다.  

Now, let's look at the route table.  
이제 라우트 테이블을 살펴봅시다.  

The route table directs traffic within your VPC.  
라우트 테이블은 VPC 내 트래픽을 안내합니다.  

The default route table, also called the main route table, has two rules.  
기본 라우트 테이블(주 라우트 테이블)에는 두 가지 규칙이 있습니다.  

One of these rules directs all traffic outside of the VPC's CIDR block to the internet gateway.  
그중 하나는 VPC CIDR 블록 외부로 향하는 모든 트래픽을 인터넷 게이트웨이로 보냅니다.  

---

The internet gateway is attached to the VPC and provides internet access to EC2 instances within the VPC.  
인터넷 게이트웨이는 VPC에 연결되어 VPC 내 EC2 인스턴스에 인터넷 접근을 제공합니다.  

This explains why our EC2 instances have internet connectivity.  
이로 인해 EC2 인스턴스가 인터넷에 연결될 수 있습니다.  

We will examine the internet gateway in more detail later in the course.  
인터넷 게이트웨이는 강좌 후반부에서 더 자세히 살펴볼 예정입니다.  

---

The route table is not explicitly associated with any subnets but is implicitly associated because the subnets do not have a specific route table assigned.  
라우트 테이블은 특정 서브넷에 명시적으로 연결되지 않았지만, 서브넷에 특정 라우트 테이블이 없으므로 암묵적으로 연결됩니다.  

Therefore, the main route table is assigned to them by default.  
따라서 기본 라우트 테이블이 자동으로 할당됩니다.  

---

In summary, we have reviewed VPCs, subnets, route tables, and the internet gateway at a high level.  
요약하면, VPC, 서브넷, 라우트 테이블, 인터넷 게이트웨이를 개략적으로 살펴보았습니다.  

This overview helps explain why we can launch EC2 instances and why they receive specific IP addresses and connectivity.  
이 개요는 EC2 인스턴스를 시작하고 IP 주소와 연결이 부여되는 이유를 설명하는 데 도움을 줍니다.  

In upcoming sections, we will spend more time examining these components and recreate our own VPC to understand their structure and function in detail.  
다음 강의에서는 이러한 구성 요소를 자세히 살펴보고 자체 VPC를 생성하여 구조와 기능을 이해할 예정입니다.  

I hope you are excited to continue, and I will see you in the next lecture.  
강의를 계속할 준비가 되었기를 바라며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- The default VPC is automatically created in new AWS accounts to simplify initial cloud usage.  
- 기본 VPC는 신규 AWS 계정에 자동 생성되어 클라우드 시작을 단순화합니다.  

- Each EC2 instance launched in the default VPC receives a public IPv4 address and DNS names, enabling immediate internet connectivity.  
- 기본 VPC에서 시작된 각 EC2 인스턴스는 공인 IPv4 주소와 DNS 이름을 받아 즉시 인터넷에 연결됩니다.  

- The default VPC includes three subnets across different availability zones for high availability.  
- 기본 VPC에는 고가용성을 위해 서로 다른 가용 영역에 세 개의 서브넷이 포함됩니다.  

- The main route table directs outbound traffic to the internet gateway, providing internet access to instances within the VPC.  
- 주 라우트 테이블은 아웃바운드 트래픽을 인터넷 게이트웨이로 안내하여 VPC 내 인스턴스가 인터넷에 접속할 수 있도록 합니다.  
```

🎮 게임보상 완료: "VPC Explorer" +300 XP 🏆
