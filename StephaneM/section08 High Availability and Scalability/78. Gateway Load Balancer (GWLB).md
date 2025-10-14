# Gateway Load Balancer (GWLB)  
# 게이트웨이 로드 밸런서 (GWLB)  
→ AWS에서 네트워크 트래픽 검사를 위해 설계된 최신 로드 밸런서입니다.  

---

## Introduction to Gateway Load Balancer  
## 게이트웨이 로드 밸런서 소개  
→ GWLB가 무엇인지 개념부터 설명합니다.  

The Gateway Load Balancer (GWLB) is the newest type of load balancer designed to deploy, scale, and manage your fleet of third-party network-neutral appliances in AWS.  
게이트웨이 로드 밸런서(GWLB)는 AWS에서 타사 네트워크 장비(방화벽, 보안 장비 등)를 배포, 확장, 관리하도록 설계된 최신 로드 밸런서입니다.  

This service is particularly useful when you want all network traffic to pass through a firewall, an intrusion detection and prevention system (IDPS), or a deep packet inspection system before reaching your applications.  
이 서비스는 모든 네트워크 트래픽이 애플리케이션에 도달하기 전에 방화벽, 침입 탐지/방지 시스템(IDPS), 패킷 심층 검사 시스템을 반드시 거치도록 하고 싶을 때 유용합니다.  

It also supports modifying payloads at the network level.  
또한 네트워크 계층에서 페이로드를 수정하는 기능도 지원합니다.  

---

## Traffic Flow with Gateway Load Balancer  
## 게이트웨이 로드 밸런서를 이용한 트래픽 흐름  
→ 일반적인 ALB 흐름과 비교해봅니다.  

Consider users accessing your applications. Typically, users connect directly to your application through a load balancer, such as an Application Load Balancer (ALB).  
사용자가 애플리케이션에 접근한다고 가정해봅시다. 보통 사용자는 ALB 같은 로드 밸런서를 통해 애플리케이션에 직접 연결합니다.  

The traffic flows directly from the users to the ALB and then to the application.  
트래픽은 사용자에서 ALB를 거쳐 애플리케이션으로 직접 전달됩니다.  

However, if you want all network traffic to be inspected before reaching your application, you can deploy third-party virtual appliances, such as EC2 instances, that analyze the traffic.  
하지만 애플리케이션에 도달하기 전에 모든 트래픽을 검사하고 싶다면 EC2 기반의 보안 장비 같은 가상 어플라이언스를 배치할 수 있습니다.  

Previously, this setup was complicated, but the Gateway Load Balancer simplifies this process.  
이전에는 이런 구성이 복잡했지만, GWLB는 이를 간단하게 만듭니다.  

---

## How Gateway Load Balancer Works  
## 게이트웨이 로드 밸런서의 동작 방식  
→ VPC 라우팅을 바꿔 트래픽을 GWLB를 거치게 만듭니다.  

When you create a Gateway Load Balancer, the route tables in your Virtual Private Cloud (VPC) are updated.  
GWLB를 생성하면 VPC 라우팅 테이블이 업데이트됩니다.  

This advanced networking configuration ensures that all user traffic first passes through the Gateway Load Balancer.  
이 설정으로 모든 사용자 트래픽이 먼저 GWLB를 거치도록 보장됩니다.  

The Gateway Load Balancer then distributes the traffic across a target group of your virtual appliances.  
GWLB는 트래픽을 가상 어플라이언스 대상 그룹으로 분배합니다.  

These appliances analyze the traffic—for example, acting as firewalls or intrusion detection systems.  
이 어플라이언스들은 트래픽을 분석하며, 예를 들어 방화벽이나 침입 탐지 장치처럼 동작할 수 있습니다.  

If the appliances approve the traffic, they send it back to the Gateway Load Balancer; if not, they can drop the traffic.  
승인된 트래픽은 다시 GWLB로 전달되고, 승인되지 않으면 차단됩니다.  

Approved traffic is forwarded by the Gateway Load Balancer to your application.  
승인된 트래픽만 애플리케이션으로 전달됩니다.  

This process is transparent to the application, with the only change being that all traffic now passes through the Gateway Load Balancer and your third-party appliances for inspection and possible filtering.  
이 과정은 애플리케이션 입장에서는 투명하게 이루어지며, 단지 모든 트래픽이 GWLB와 보안 장비를 거친다는 차이가 있습니다.  

---

## Operating Layer and Protocol  
## 동작 계층 및 프로토콜  
→ 어떤 계층에서 어떻게 트래픽을 다루는지 설명합니다.  

The Gateway Load Balancer operates at Layer 3, the network layer, handling IP packets.  
GWLB는 OSI 3계층(네트워크 계층)에서 동작하며 IP 패킷을 처리합니다.  

It serves two main functions:  
GWLB의 주요 기능은 두 가지입니다:  

Acts as a transparent network gateway, providing a single entry and exit point for all traffic in your VPC.  
1. VPC 내 모든 트래픽의 단일 입출구 역할을 하는 투명한 네트워크 게이트웨이 기능  

Functions as a load balancer by distributing traffic across a set of virtual appliances in your target group.  
2. 대상 그룹 내 여러 가상 어플라이언스로 트래픽을 분산하는 로드 밸런서 기능  

Importantly, the Gateway Load Balancer uses the GENEVE protocol on port 6081 for encapsulating and forwarding traffic to the appliances.  
중요하게도 GWLB는 트래픽을 캡슐화·전송하기 위해 포트 6081의 GENEVE 프로토콜을 사용합니다.  

---

## Target Groups for Gateway Load Balancer  
## 게이트웨이 로드 밸런서의 대상 그룹  
→ GWLB가 트래픽을 분산할 대상을 정의합니다.  

The target groups for the Gateway Load Balancer consist of your third-party appliances.  
GWLB 대상 그룹은 주로 타사 보안 장비(어플라이언스)로 구성됩니다.  

These can be:  
대상에는 다음이 포함될 수 있습니다:  

EC2 instances registered by instance ID.  
- 인스턴스 ID로 등록된 EC2 인스턴스  

Private IP addresses, which is useful if you are running virtual appliances in your own data center or on-premises network.  
- 프라이빗 IP 주소 (온프레미스 데이터센터나 사내 네트워크의 가상 어플라이언스와 연동 가능)  

This flexibility allows integration of both cloud-based and on-premises appliances for traffic inspection.  
이러한 유연성 덕분에 클라우드 및 온프레미스 보안 장비를 모두 트래픽 검사에 활용할 수 있습니다.  

---

## Summary  
## 요약  
→ 핵심 내용을 간단히 정리합니다.  

The Gateway Load Balancer simplifies the deployment and management of network traffic inspection appliances by routing all traffic through these devices transparently.  
GWLB는 모든 네트워크 트래픽을 보안 장비로 투명하게 라우팅함으로써 보안 장비의 배치 및 관리 과정을 단순화합니다.  

Understanding the traffic flow diagram and the role of the Gateway Load Balancer at the network layer is crucial for grasping its functionality.  
트래픽 흐름과 네트워크 계층에서의 GWLB 역할을 이해하는 것이 핵심입니다.  

While hands-on configuration can be complex, a high-level understanding is sufficient for most practical and exam purposes.  
직접 구성은 다소 복잡할 수 있으나, 개념적인 이해만으로도 실무 및 시험에 충분합니다.  

---

## Key Takeaways  
## 핵심 요약  
→ 시험이나 실무에서 꼭 알아야 할 포인트입니다.  

- The Gateway Load Balancer (GWLB) enables deployment, scaling, and management of third-party network appliances in AWS.  
  GWLB는 AWS에서 타사 네트워크 장비를 배포, 확장, 관리할 수 있게 해줍니다.  

- GWLB directs all network traffic through virtual appliances such as firewalls or intrusion detection systems before reaching applications.  
  GWLB는 애플리케이션에 도달하기 전에 모든 트래픽을 방화벽이나 침입 탐지 장비 같은 가상 어플라이언스를 통해 전달합니다.  

- It operates at the network layer (Layer 3) using the GENEVE protocol on port 6081.  
  GWLB는 네트워크 계층(Layer 3)에서 동작하며, 포트 6081의 GENEVE 프로토콜을 사용합니다.  

- Target groups for GWLB can be EC2 instances or private IP addresses, including appliances in on-premises data centers.  
  GWLB의 대상 그룹은 EC2 인스턴스나 프라이빗 IP일 수 있으며, 온프레미스 데이터센터의 장비도 포함할 수 있습니다.  

---

이제 이 내용을 **`.md` 파일**로 저장하면 됩니다.
👉 게임 보상: 🛡️ **“네트워크 수호자” 칭호 획득!** 🎮

저장용 `.md` 파일 만들어드릴까?
