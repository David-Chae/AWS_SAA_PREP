AWS Global Accelerator는 전 세계 사용자들에게 **애플리케이션의 접속 속도를 높이고 안정성을 확보**하기 위해 AWS의 **고속 글로벌 네트워크**를 활용하는 서비스입니다.

쉽게 말해, 느리고 불안정한 **일반 인터넷 구간** 대신, 빠르고 안정적인 **AWS 전용 고속도로**를 이용해 사용자 트래픽을 서버까지 전달하는 것입니다.

---

## 1. 🌐 Global Accelerator가 해결하려는 문제

만약 여러분의 애플리케이션 서버가 인도(India) 한 곳에만 배포되어 있는데, 사용자들이 미국, 유럽, 호주 등 전 세계에 퍼져있다고 가정해 봅시다.

* **문제점:** 이 먼 거리의 사용자들이 인도 서버에 접속하려면 트래픽이 **일반 공용 인터넷**을 통해 수많은 라우터(Router)를 거쳐가야 합니다.
    * **느린 속도 (Latency):** 여러 단계를 거치면서 속도가 느려집니다.
    * **높은 불안정성:** 연결이 끊기거나 데이터가 손실될 위험이 높아집니다.
    * **비효율적인 경로:** 최적의 경로로 가지 못하고 우회하는 경우가 많습니다.

Global Accelerator의 목표는 사용자가 가능한 한 빨리 **AWS의 전용 네트워크 내부**로 들어오게 하여, 느린 공용 인터넷 구간을 최소화하는 것입니다.



---

## 2. ⚡️ 핵심 작동 원리: Anycast IP와 AWS 전용 네트워크

Global Accelerator는 두 가지 핵심 기술을 사용합니다.

### A. Anycast IP (애니캐스트 IP) 활용
* **일반적인 유니캐스트(Unicast) IP:** 하나의 서버가 하나의 고유한 IP 주소를 가집니다.
* **애니캐스트(Anycast) IP:** **여러 서버가 하나의 동일한 IP 주소를 공유**합니다.
    * 사용자가 이 Anycast IP로 접속하면, 네트워크는 자동으로 **가장 가까운 거점 서버**로 사용자를 연결해 줍니다.

Global Accelerator는 여러분의 애플리케이션에 **두 개의 고정된(Static) Anycast IP 주소**를 부여합니다. 전 세계 사용자는 이 IP 주소로 접속하게 됩니다.

### B. AWS 글로벌 네트워크 사용
1.  **사용자 접속:** 미국 사용자가 Anycast IP로 접속하면, 요청은 **가장 가까운 AWS 거점(Edge Location)**으로 라우팅됩니다. (예: 미국의 거점)
2.  **전용 네트워크 이동:** 거점에 도착한 트래픽은 **공용 인터넷을 떠나**, **AWS의 빠르고 사설적인 글로벌 네트워크**를 타고 목적지 서버(예: 인도의 ALB)까지 직접 이동합니다.
3.  **결과:** 사용자는 공용 인터넷을 짧게 이용하고, 대부분의 거리는 AWS의 고속도로를 이용하므로 **연결 속도가 빠르고 안정적**입니다.

---

## 3. 🎯 Global Accelerator의 주요 특징

| 특징 | 설명 |
| :--- | :--- |
| **정적 IP 주소 제공** | 전 세계 어디서 접속하든 단 **두 개의 고정된 외부 IP 주소**만 사용합니다. 이는 클라이언트의 방화벽 설정(Whitelist)을 간편하게 만듭니다. |
| **빠른 장애 조치 (Failover)** | Global Accelerator는 서버 엔드포인트(ALB, EC2 등)의 상태를 **Health Check**로 지속적으로 확인합니다. 만약 문제가 발생하면 **1분 이내**에 자동으로 건강한 다른 리전/엔드포인트로 트래픽을 전환합니다. (재해 복구에 탁월) |
| **다양한 서버 지원** | **ALB, NLB, EC2 인스턴스, Elastic IP** 등 다양한 AWS 리소스를 엔드포인트로 사용할 수 있습니다. (공개/비공개 모두 가능) |
| **보안 강화** | **AWS Shield**와 통합되어 자동으로 **DDoS 공격 방어** 기능을 제공합니다. |

---

## 4. 🔄 CloudFront와의 차이점 (중요!)

Global Accelerator와 CloudFront는 모두 AWS 글로벌 네트워크와 거점을 사용하지만, **목적과 처리하는 트래픽 종류**가 다릅니다.

| 구분 | Global Accelerator | CloudFront |
| :--- | :--- | :--- |
| **주요 목적** | **TCP/UDP 트래픽**의 **경로 최적화** 및 **고속화** (캐싱 없음) | **HTTP/HTTPS 콘텐츠**의 **캐싱**을 통한 성능 향상 |
| **작동 방식** | 거점에서 서버까지 패킷을 **프록시(Proxy)** 방식으로 전달 | 거점에서 콘텐츠를 **저장(Cache)** 후 전달 (필요 시에만 원본 접속) |
| **적합한 사용처** | **캐싱이 어려운 애플리케이션:** 게이밍, IoT, Voip, 동영상 스트리밍, API 등 | **캐싱이 가능한 콘텐츠:** 이미지, 동영상, CSS, HTML 등 |
| **IP 주소** | **고정된(Static) Anycast IP**를 제공 | 요청 시마다 달라질 수 있는 **동적(Dynamic) DNS** 주소를 사용 |


# AWS Global Accelerator - Overview  
# AWS 글로벌 액셀러레이터 - 개요  

---

In this lecture, we will discuss a newer AWS service called the AWS Global Accelerator.  
이번 강의에서는 AWS의 최신 서비스인 AWS 글로벌 액셀러레이터에 대해 다룹니다.  
> 글로벌 트래픽 가속화와 지연 시간 최소화 서비스 소개.  

Before diving into the details, I want to introduce the problem it aims to solve and how it addresses it.  
세부 내용에 들어가기 전에, 이 서비스가 해결하려는 문제와 접근 방식을 먼저 소개합니다.  
> 서비스 필요성 및 문제 정의.  

Imagine you have deployed a global application with users all over the world, but your application is deployed only in one AWS region.  
전 세계에 사용자가 있는 글로벌 애플리케이션이 있지만, 애플리케이션이 한 AWS 리전에서만 배포되어 있다고 가정합니다.  
> 전 세계 사용자 대상 단일 리전 배포 시 문제 발생.  

For example, the application is deployed in India, but users are located in America, Europe, and Australia.  
예를 들어, 애플리케이션은 인도 리전에 배포되어 있지만, 사용자는 미국, 유럽, 호주에 있습니다.  

When these users access the application, their traffic travels over the public internet, which can add significant latency due to multiple hops through routers.  
사용자가 애플리케이션에 접속하면 트래픽이 공용 인터넷을 통과하며, 라우터 여러 단계를 거치면서 지연 시간이 증가할 수 있습니다.  
> 공용 인터넷 경유 시 지연 시간과 연결 불안정 위험.  

For instance, users in America might experience five hops through routers before reaching the public Application Load Balancer (ALB) in India.  
예를 들어, 미국 사용자는 인도의 공용 ALB에 도달하기 전에 다섯 번의 라우터 홉을 경험할 수 있습니다.  

Similarly, users in Australia and Europe face many hops.  
마찬가지로 호주와 유럽의 사용자도 여러 홉을 거칩니다.  

These hops introduce latency, increase the risk of lost connections, and are not the most direct path into Amazon's infrastructure.  
이 홉들은 지연 시간을 증가시키고 연결 손실 위험을 높이며, 아마존 인프라로의 최적 경로가 아닙니다.  

Our goal is to route traffic as quickly as possible through the AWS global network to minimize latency.  
목표는 AWS 글로벌 네트워크를 통해 트래픽을 가능한 빨리 라우팅하여 지연 시간을 최소화하는 것입니다.  

Before explaining how Global Accelerator achieves this, let's review the concepts of Unicast and Anycast IP addresses.  
Global Accelerator가 이를 달성하는 방법을 설명하기 전에, Unicast와 Anycast IP 개념을 먼저 살펴봅니다.  

---

## Unicast IP  
## 유니캐스트 IP  

Unicast IP is the traditional IP addressing method where one server holds one unique IP address.  
유니캐스트 IP는 한 서버가 하나의 고유 IP 주소를 가지는 전통적인 IP 주소 방식입니다.  

For example, if one server has the IP address starting with 12 and another has 98, clients connecting to IP 12 will reach the first server, and those connecting to IP 98 will reach the second server.  
예를 들어, 한 서버의 IP가 12로 시작하고 다른 서버가 98이라면, IP 12에 연결된 클라이언트는 첫 번째 서버에, IP 98에 연결된 클라이언트는 두 번째 서버에 도달합니다.  
> 서버별 고유 IP 연결 방식.  

---

## Anycast IP  
## 애니캐스트 IP  

Anycast IP differs in that multiple servers share the same IP address.  
애니캐스트 IP는 여러 서버가 동일한 IP 주소를 공유하는 방식입니다.  

When a client connects to this Anycast IP, the network routes the client to the nearest server holding that IP.  
클라이언트가 애니캐스트 IP에 연결하면, 네트워크가 클라이언트를 해당 IP를 가진 가장 가까운 서버로 라우팅합니다.  
> 네트워크 지형을 기반으로 자동 최적 경로 지정.  

Although this may seem counterintuitive, it is how Anycast works.  
직관과 다르게 보이지만, 이것이 애니캐스트의 작동 원리입니다.  

Clients are automatically directed to the closest server based on network topology.  
클라이언트는 네트워크 토폴로지를 기반으로 가장 가까운 서버로 자동 연결됩니다.  

---

AWS Global Accelerator leverages the Anycast IP concept.  
AWS 글로벌 액셀러레이터는 애니캐스트 IP 개념을 활용합니다.  

Instead of sending traffic over the public internet, user requests are routed to the closest AWS edge location.  
사용자 요청은 공용 인터넷을 거치지 않고 가장 가까운 AWS 엣지 위치로 라우팅됩니다.  

From there, traffic travels over the private AWS global network directly to your application endpoint, such as an ALB in India.  
그 후 트래픽은 AWS 글로벌 프라이빗 네트워크를 통해 직접 애플리케이션 엔드포인트(예: 인도의 ALB)로 전달됩니다.  
> 지연 시간 최소화 및 안정적인 트래픽 전달.  

For example, a user in America connects to the Anycast IP, which routes the request to the nearest AWS edge location in America.  
예를 들어, 미국 사용자가 애니캐스트 IP에 연결하면, 요청은 미국 내 가장 가까운 AWS 엣지 위치로 라우팅됩니다.  

The traffic then travels over the AWS internal network to the ALB in India.  
그 트래픽은 AWS 내부 네트워크를 통해 인도의 ALB로 전달됩니다.  

Similarly, users in Australia and Europe connect to their closest edge locations, and traffic is routed privately to the application.  
마찬가지로 호주와 유럽 사용자도 가장 가까운 엣지 위치에 연결되고, 트래픽은 애플리케이션으로 프라이빗하게 라우팅됩니다.  

---

Global Accelerator provides two static Anycast IP addresses for your application globally.  
Global Accelerator는 애플리케이션 전용으로 두 개의 고정 애니캐스트 IP를 제공합니다.  

These IPs route traffic to the closest edge location of your users, which then forwards the traffic through the private AWS network to your application.  
이 IP는 사용자와 가장 가까운 엣지 위치로 트래픽을 라우팅하고, 이후 AWS 프라이빗 네트워크를 통해 애플리케이션으로 전달됩니다.  

This approach offers a more stable and lower latency connection compared to the public internet.  
이 접근 방식은 공용 인터넷보다 안정적이고 낮은 지연 시간을 제공합니다.  

---

The service supports various AWS resources including Elastic IPs, EC2 instances, Application Load Balancers, and Network Load Balancers, whether they are public or private.  
이 서비스는 Elastic IP, EC2, ALB, NLB 등 공개/비공개 AWS 리소스를 모두 지원합니다.  

It ensures consistent performance by using intelligent routing to the lowest latency edge location and provides fast regional failover in case of issues.  
낮은 지연 시간 엣지 위치로 지능형 라우팅을 사용하여 안정적인 성능을 제공하며, 문제가 발생하면 빠른 지역 장애 조치를 수행합니다.  

Global Accelerator performs health checks on your application endpoints.  
Global Accelerator는 애플리케이션 엔드포인트에 대해 헬스체크를 수행합니다.  

If a health check fails for one ALB or region, it automatically fails over to a healthy endpoint in less than one minute.  
ALB 또는 리전의 헬스체크가 실패하면, 1분 이내에 자동으로 정상 엔드포인트로 장애 조치를 수행합니다.  

This feature is excellent for disaster recovery scenarios.  
이 기능은 재해 복구 시나리오에 매우 유용합니다.  

From a security perspective, Global Accelerator is well secured because only two external IP addresses need to be whitelisted by your clients.  
보안 측면에서, Global Accelerator는 클라이언트가 두 개의 외부 IP만 화이트리스트에 등록하면 되어 보안성이 높습니다.  

Additionally, it provides automatic DDoS protection through AWS Shield, enhancing your application's security posture.  
또한 AWS Shield를 통한 자동 DDoS 보호 기능으로 애플리케이션 보안을 강화합니다.  

---

## Difference Between Global Accelerator and CloudFront  
## 글로벌 액셀러레이터와 CloudFront 차이  

Both Global Accelerator and CloudFront use the same AWS global network and edge locations and integrate with AWS Shield for DDoS protection.  
Global Accelerator와 CloudFront 모두 동일한 AWS 글로벌 네트워크와 엣지 위치를 사용하며 AWS Shield와 통합되어 DDoS 보호 기능을 제공합니다.  

However, their purposes differ significantly.  
하지만 목적은 크게 다릅니다.  

CloudFront improves performance primarily for cacheable content such as images and videos, as well as dynamic content like API acceleration and dynamic site delivery.  
CloudFront는 이미지, 비디오 같은 캐시 가능한 콘텐츠와 API 가속, 동적 사이트 전달 같은 동적 콘텐츠 성능 향상에 초점을 맞춥니다.  

Content is served from edge locations, which occasionally fetch content from the origin but mostly deliver cached content.  
콘텐츠는 엣지 위치에서 제공되며, 가끔 오리진에서 가져오지만 대부분 캐시된 콘텐츠를 전달합니다.  

In contrast, Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets from edge locations to applications running in one or more AWS regions.  
반면 Global Accelerator는 TCP/UDP 트래픽을 엣지 위치에서 AWS 리전 내 애플리케이션으로 프록시하여 광범위한 애플리케이션 성능을 향상시킵니다.  

There is no caching involved, making it ideal for non-HTTP use cases such as gaming, IoT, or Voice over IP, as well as HTTP use cases requiring static global IP addresses or deterministic, fast regional failover.  
캐싱이 없으므로 게임, IoT, VoIP 같은 비HTTP 사용 사례와 고정 글로벌 IP 또는 빠른 지역 장애 조치가 필요한 HTTP 사용 사례에 적합합니다.  

Global Accelerator is a newer AWS service and is important for AWS certification exams.  
Global Accelerator는 최신 AWS 서비스로, AWS 인증 시험에서 중요합니다.  

This concludes the lecture on AWS Global Accelerator.
이로써 AWS 글로벌 액셀러레이터 강의를 마칩니다.

In the next lecture, we will have a hands-on session.
다음 강의에서는 실습 세션이 예정되어 있습니다.

---

## Key Takeaways

## 핵심 요약

* AWS Global Accelerator uses Anycast IP addresses to route user traffic to the nearest AWS edge location, reducing latency by leveraging the AWS global network.

* AWS 글로벌 액셀러레이터는 애니캐스트 IP를 사용하여 사용자 트래픽을 가장 가까운 AWS 엣지 위치로 라우팅하며, 글로벌 네트워크를 활용하여 지연 시간을 줄입니다.

* It supports multiple AWS resources including Elastic IPs, EC2 instances, Application Load Balancers, and Network Load Balancers, whether public or private.

* Elastic IP, EC2, ALB, NLB 등 공개/비공개 AWS 리소스를 지원합니다.

* Global Accelerator provides consistent performance, fast regional failover, health checks, and integrated DDoS protection via AWS Shield.

* 안정적인 성능, 빠른 지역 장애 조치, 헬스체크, AWS Shield를 통한 DDoS 보호 기능을 제공합니다.

* The service differs from CloudFront by proxying TCP/UDP traffic without caching, making it suitable for non-HTTP use cases and applications requiring static global IP addresses.

* TCP/UDP 트래픽을 캐싱 없이 프록시하며, 비HTTP 사용 사례와 고정 글로벌 IP가 필요한 애플리케이션에 적합합니다.


🎮 **게임보상:**  
- AWS Global Accelerator 이해 +15 XP  
- Anycast IP와 지연 시간 최적화 이해 +10 XP  
- CloudFront와 차이점 이해 +10 XP  
총 **35 XP 획득!** 🎉
