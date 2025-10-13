# Network Load Balancer (NLB)  
# 네트워크 로드 밸런서 (NLB)  
➡️ 이번에는 **NLB의 기본 개념과 특징**을 다룹니다.  
🎁 보상: ✅ 기초 이해 포인트 +5  

---

## Introduction to Network Load Balancer  
## 네트워크 로드 밸런서 소개  
➡️ NLB의 기본 정의와 동작 계층을 설명합니다.  

The Network Load Balancer (NLB) operates at Layer 4 of the OSI model.  
네트워크 로드 밸런서(NLB)는 OSI 모델의 4계층(전송 계층)에서 동작합니다.  
➡️ OSI 7계층 중 **Layer 4** 담당.  
🎁 보상: 🔑 계층 지식 +10  

It allows you to manage TCP and UDP traffic, which are transport layer protocols.  
이는 전송 계층 프로토콜인 TCP와 UDP 트래픽을 관리할 수 있습니다.  
➡️ TCP/UDP는 ALB가 처리하지 않는 부분.  

This is in contrast to Layer 7 load balancers that handle HTTP traffic.  
이는 HTTP 트래픽을 처리하는 7계층 로드 밸런서와 대조됩니다.  
➡️ NLB(4계층) ↔ ALB(7계층) 비교.  

Therefore, when you encounter UDP or TCP traffic in an exam context, you should think of the Network Load Balancer.  
따라서 시험에서 UDP나 TCP 트래픽 관련 문제가 나오면 NLB를 떠올려야 합니다.  
➡️ 시험 포인트.  
🎁 보상: 🎯 시험 대비 포인트 +15  

NLB is designed for extremely high performance.  
NLB는 초고성능을 위해 설계되었습니다.  
➡️ 성능 지향형.  

It can handle millions of requests per second while maintaining ultra-low latency.  
이는 초저지연 상태로 초당 수백만 요청을 처리할 수 있습니다.  
➡️ 대규모 트래픽 환경 적합.  

This makes it suitable for applications requiring high throughput and minimal delay.  
따라서 높은 처리량과 낮은 지연이 필요한 애플리케이션에 적합합니다.  
➡️ 금융, 게임, 통신 등에서 활용.  
🎁 보상: ⚡ 성능 이해 보너스 +20  

---

## Static IP Addresses and Elastic IPs  
## 고정 IP 주소와 탄력적 IP  
➡️ NLB만의 고유 기능 설명.  

A unique feature of the Network Load Balancer is that it provides one static IP address per availability zone.  
NLB의 고유한 특징은 가용 영역(Availability Zone)마다 하나의 고정 IP를 제공한다는 점입니다.  
➡️ ALB와 차별점.  

You can assign an Elastic IP to each availability zone, which is especially useful when your application needs to be exposed through a fixed set of IP addresses.  
각 가용 영역에 탄력적 IP를 할당할 수 있으며, 이는 고정된 IP로 애플리케이션을 노출해야 할 때 유용합니다.  
➡️ IP 기반 접근 통제가 필요한 경우 적합.  

This capability is important if your application must be accessed only via one, two, or three specific IP addresses.  
애플리케이션이 특정 고정 IP 주소(1~3개)만 통해 접근 가능해야 한다면 매우 중요합니다.  
➡️ 방화벽 정책과 연계 가능.  
🎁 보상: 🛡️ 보안 강화 포인트 +15  

In exam scenarios, if you see requirements for extreme performance with TCP or UDP traffic or the need for static IPs, the Network Load Balancer should be your consideration.  
시험에서 TCP/UDP 고성능 처리와 고정 IP가 요구된다면, 답은 NLB입니다.  
➡️ 시험 키워드: TCP/UDP + Static IP.  
🎁 보상: 🎯 시험 대비 포인트 +10  

---

## How Network Load Balancer Works  
## 네트워크 로드 밸런서 작동 방식  
➡️ ALB와 유사하지만 Layer 4 중심.  

The Network Load Balancer functions similarly to the Application Load Balancer in that it uses target groups.  
NLB는 ALB와 유사하게 타겟 그룹을 사용합니다.  
➡️ 기본 구조 동일.  

You create target groups, and the NLB redirects traffic to them.  
타겟 그룹을 생성하면, NLB가 트래픽을 해당 그룹으로 전달합니다.  
➡️ 라우팅 단위 = 타겟 그룹.  

For example, the front end can use TCP traffic, while the backend might use GTP or other protocols.  
예를 들어, 프론트엔드는 TCP를, 백엔드는 GTP 같은 다른 프로토콜을 사용할 수 있습니다.  
➡️ 다양한 전송 계층 프로토콜 지원.  
🎁 보상: ⚙️ 아키텍처 이해 포인트 +15  

---

## Target Groups  
## 타겟 그룹  
➡️ EC2 및 IP 기반 지원.  

Target groups can consist of EC2 instances.  
타겟 그룹은 EC2 인스턴스로 구성할 수 있습니다.  
➡️ 가장 일반적 사용.  

This means the Network Load Balancer can redirect TCP or UDP traffic directly to your EC2 instances.  
즉, NLB는 TCP/UDP 트래픽을 EC2 인스턴스로 직접 전달할 수 있습니다.  
➡️ EC2 레벨 트래픽 제어 가능.  

Additionally, you can register IP addresses in the target groups. These IP addresses must be hard-coded and private.  
또한 타겟 그룹에 IP 주소를 등록할 수 있으며, 이 IP는 고정된 사설 IP여야 합니다.  
➡️ 외부 데이터 센터와 연동 가능.  

This allows you to send traffic to private IPs of EC2 instances you own or to private IPs of servers in your own data center. Both can be fronted by the same Network Load Balancer.  
이를 통해 소유한 EC2 인스턴스의 사설 IP 또는 온프레미스 서버의 사설 IP로 트래픽을 보낼 수 있습니다. 두 경우 모두 동일한 NLB로 처리 가능합니다.  
➡️ 하이브리드 아키텍처 지원.  
🎁 보상: 🌐 네트워크 통합 포인트 +20  

It is also possible to place a Network Load Balancer in front of an Application Load Balancer.  
NLB를 ALB 앞단에 두는 것도 가능합니다.  
➡️ 다단계 구조 설계.  

In this setup, the NLB provides fixed IP addresses, while the ALB handles HTTP traffic routing rules.  
이 구조에서 NLB는 고정 IP를 제공하고, ALB는 HTTP 라우팅 규칙을 처리합니다.  
➡️ 역할 분담 구조.  

This combination is valid and useful for certain architectures.  
이 조합은 특정 아키텍처에서 매우 유용합니다.  
➡️ 예: IP 기반 방화벽 + 세밀한 HTTP 라우팅.  
🎁 보상: 🏗️ 아키텍처 설계 포인트 +15  

---

## Health Checks  
## 상태 검사  
➡️ 서비스 안정성을 위한 핵심 요소.  

For the exam, it is important to know that the health checks performed by Network Load Balancer target groups support three protocols: TCP, HTTP, and HTTPS.  
시험에서 알아야 할 점은, NLB 타겟 그룹의 상태 검사가 TCP, HTTP, HTTPS 3가지 프로토콜을 지원한다는 것입니다.  
➡️ 단순 TCP 확인 외에도 웹 레벨 검사 가능.  
🎁 보상: ❤️ 안정성 포인트 +10  

If your backend application supports HTTP or HTTPS, you can define health checks using these protocols.  
백엔드 애플리케이션이 HTTP/HTTPS를 지원한다면 해당 프로토콜을 활용한 상태 검사를 설정할 수 있습니다.  
➡️ 세밀한 상태 관리 가능.  

---

## Conclusion  
## 결론  
➡️ 전체 요약 정리.  

This concludes the overview of the Network Load Balancer.  
이것으로 NLB 개요를 마칩니다.  

It is a high-performance Layer 4 load balancer that supports TCP and UDP traffic, provides static IP addresses per availability zone, supports target groups with EC2 instances or private IPs, and allows health checks over TCP, HTTP, and HTTPS protocols.  
NLB는 고성능 Layer 4 로드 밸런서로, TCP/UDP 트래픽 지원, 가용 영역당 고정 IP 제공, EC2/사설 IP 기반 타겟 그룹 지원, TCP/HTTP/HTTPS 상태 검사를 제공합니다.  
➡️ 핵심 요약: 성능 + 고정 IP + 유연성 + 안정성.  
🎁 보상: 🏆 NLB 마스터 포인트 +30  

---

## Key Takeaways  
## 핵심 요약  
➡️ 시험 대비 및 실무 핵심 정리.  

- Network Load Balancer (NLB) operates at Layer 4, handling TCP and UDP traffic.  
- NLB는 Layer 4에서 동작하며, TCP/UDP 트래픽을 처리합니다.  
🎁 보상: ✅ 핵심 개념 포인트 +10  

- NLB provides ultra-high performance with the ability to handle millions of requests per second and ultra-low latency.  
- 초당 수백만 요청 처리와 초저지연 성능을 제공합니다.  
🎁 보상: ⚡ 성능 이해 포인트 +10  

- Each availability zone in NLB has one static IP, and elastic IPs can be assigned for static IP exposure.  
- 가용 영역마다 고정 IP를 가지며, 탄력적 IP를 할당할 수 있습니다.  
🎁 보상: 🛡️ 보안 포인트 +10  

- NLB supports target groups consisting of EC2 instances or hard-coded private IP addresses, including those from on-premises data centers.  
- EC2 인스턴스나 온프레미스 사설 IP 기반 타겟 그룹을 지원합니다.  
🎁 보상: 🌐 네트워크 확장 포인트 +10  

- NLB can be used in front of an Application Load Balancer (ALB) to combine fixed IP addresses with HTTP traffic routing rules.  
- NLB를 ALB 앞에 두어 고정 IP와 HTTP 라우팅을 결합할 수 있습니다.  
🎁 보상: 🏗️ 아키텍처 포인트 +10  

- Health checks for NLB target groups support TCP, HTTP, and HTTPS protocols.  
- NLB 상태 검사는 TCP, HTTP, HTTPS 프로토콜을 지원합니다.  
🎁 보상: ❤️ 안정성 포인트 +10  

---

제가 번역 + 설명 + 게임보상(✅ 포인트, ⚡ 보너스, 🏆 마스터 포인트 등)을 포함해서 정리했습니다.

👉 혹시 보상을 RPG 스타일(예: 경험치, 골드, 아이템 드랍)로 바꿔드릴까요, 아니면 지금처럼 **지식 포인트 시스템**을 유지할까요?
