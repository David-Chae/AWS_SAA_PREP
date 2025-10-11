# Elastic Load Balancing (ELB) Overview  
# 탄력적 로드 밸런싱(ELB) 개요  

---

## Introduction to Load Balancing  
## 로드 밸런싱 소개  

Let's learn about load balancing.  
로드 밸런싱에 대해 배워봅시다.  

A load balancer is a server or a set of servers that forward received traffic to multiple backend or downstream EC2 instances or servers.  
로드 밸런서는 들어오는 트래픽을 여러 개의 백엔드 EC2 인스턴스나 서버로 전달하는 서버 혹은 서버 집합입니다.  

For example, imagine three EC2 instances fronted by an Elastic Load Balancer, which is a set of servers behind the scenes.  
예를 들어, 세 개의 EC2 인스턴스 앞에 ELB(Elastic Load Balancer)가 있다고 가정해 봅시다. ELB는 내부적으로 서버 집합입니다.  

When three users connect directly to your Elastic Load Balancer, the first user's load is sent to one backend EC2 instance.  
세 명의 사용자가 ELB에 접속하면, 첫 번째 사용자의 요청은 한 개의 EC2 인스턴스로 전송됩니다.  

Because of load balancing, the second user is sent to another EC2 instance, and the third user is sent to the third EC2 instance.  
로드 밸런싱 덕분에 두 번째 사용자는 다른 EC2 인스턴스로, 세 번째 사용자는 또 다른 인스턴스로 전송됩니다.  

The more users you have, the more the load is balanced across EC2 instances.  
사용자가 많아질수록 부하는 여러 EC2 인스턴스에 고르게 분산됩니다.  

Users do not know which backend instances they are connected to; they only connect to the Elastic Load Balancer, which provides a single endpoint for connectivity.  
사용자는 자신이 어떤 인스턴스에 연결되는지 알 수 없으며, ELB가 제공하는 단일 접속 지점에만 연결됩니다.  

---

## Benefits of Using a Load Balancer  
## 로드 밸런서 사용의 장점  

Using a load balancer to spread load across multiple downstream instances offers several advantages:  
로드 밸런서를 사용하여 부하를 여러 인스턴스에 분산하면 여러 장점이 있습니다:  

- Provides a single point of access to your applications.  
- 애플리케이션에 단일 접속 지점을 제공합니다.  

- Seamlessly handles failures of downstream instances through health check mechanisms.  
- 헬스 체크 메커니즘으로 인스턴스 장애를 자동으로 처리합니다.  

- Supports health checks to determine instance availability.  
- 인스턴스의 가용성을 확인하는 헬스 체크를 지원합니다.  

- Provides SSL termination for HTTPS encrypted traffic.  
- HTTPS 암호화 트래픽을 위한 SSL 종료 기능을 제공합니다.  

- Enforces stickiness with cookies.  
- 쿠키를 사용해 세션 지속성(스티키니스)을 유지할 수 있습니다.  

- Ensures high availability across zones.  
- 여러 가용 영역(AZ)에 걸쳐 고가용성을 보장합니다.  

- Separates public traffic from private traffic in your cloud environment.  
- 클라우드 환경에서 공용 트래픽과 사설 트래픽을 분리합니다.  

The Elastic Load Balancer is a managed load balancer.  
ELB는 관리형 로드 밸런서입니다.  

AWS manages it, guaranteeing its operation regardless of circumstances.  
AWS가 이를 관리하며 어떤 상황에서도 운영을 보장합니다.  

AWS handles upgrades, maintenance, and high availability, while providing configuration options to tweak load balancer behavior.  
AWS는 업그레이드, 유지보수, 고가용성을 관리하며, 로드 밸런서 동작을 조정할 수 있는 옵션도 제공합니다.  

Using an Elastic Load Balancer is cost-effective compared to setting up your own load balancer.  
ELB를 사용하는 것이 자체 로드 밸런서를 구축하는 것보다 비용 효율적입니다.  

Managing your own load balancer can be a nightmare from a scalability perspective.  
자체 로드 밸런서를 관리하는 것은 확장성 측면에서 악몽이 될 수 있습니다.  

Additionally, the load balancer integrates with many AWS services such as EC2 instances, scaling groups, Amazon ECS, Certificate Manager, CloudWatch, Route 53, WAF, Global Accelerator, and more.  
또한 ELB는 EC2, 오토 스케일링 그룹, ECS, Certificate Manager, CloudWatch, Route 53, WAF, Global Accelerator 등 다양한 AWS 서비스와 통합됩니다.  

---

## Health Checks  
## 헬스 체크  

Health checks allow your Elastic Load Balancer to verify whether an EC2 instance is functioning properly.  
헬스 체크는 ELB가 EC2 인스턴스가 정상 작동하는지 확인할 수 있도록 합니다.  

If an instance is unhealthy, the load balancer will not send traffic to it.  
인스턴스가 비정상이면 로드 밸런서는 트래픽을 보내지 않습니다.  

Health checks are performed using a port and route.  
헬스 체크는 특정 포트와 경로를 사용해 수행됩니다.  

For example, the protocol could be HTTP, the port 4567, and the endpoint /health which is an application route to check health status.  
예: 프로토콜은 HTTP, 포트는 4567, 엔드포인트는 `/health`일 수 있습니다. 이 경로로 애플리케이션의 상태를 확인합니다.  

If the EC2 instance does not respond with an OK response, usually HTTP status code 200, it is marked unhealthy and excluded from traffic routing.  
EC2 인스턴스가 정상 응답(보통 HTTP 200)을 반환하지 않으면 비정상으로 표시되고 트래픽에서 제외됩니다.  

---

## Types of Managed Load Balancers on AWS  
## AWS 관리형 로드 밸런서 유형  

AWS provides four kinds of managed load balancers:  
AWS는 네 가지 관리형 로드 밸런서를 제공합니다:  

- **Classic Load Balancer (CLB):** Older generation from 2009, supports HTTP, HTTPS, TCP, SSL, and Secure TCP. It is deprecated and shown as such in the AWS console but still available.  
- **Classic Load Balancer (CLB):** 2009년에 도입된 구세대, HTTP, HTTPS, TCP, SSL, Secure TCP를 지원합니다. 현재 사용 중단 상태로 표시되지만 여전히 이용 가능합니다.  

- **Application Load Balancer (ALB):** Introduced around 2016, supports HTTP, HTTPS, and WebSocket protocols.  
- **Application Load Balancer (ALB):** 2016년경 도입, HTTP, HTTPS, WebSocket 프로토콜을 지원합니다.  

- **Network Load Balancer (NLB):** Introduced in 2017, supports TCP, TLS, Secure TCP, and UDP protocols.  
- **Network Load Balancer (NLB):** 2017년 도입, TCP, TLS, Secure TCP, UDP 프로토콜을 지원합니다.  

- **Gateway Load Balancer (GWLB):** Introduced in 2020, operates at the network layer and supports the IP protocol.  
- **Gateway Load Balancer (GWLB):** 2020년 도입, 네트워크 계층에서 동작하며 IP 프로토콜을 지원합니다.  

It is recommended to use the newer generation load balancers as they provide more features.  
새로운 세대의 로드 밸런서를 사용하는 것이 더 많은 기능을 제공하므로 권장됩니다.  

Load balancers can be configured as internal (private) for private network access or external (public) for websites and public applications.  
로드 밸런서는 사설 네트워크 접근을 위한 내부형 또는 웹사이트와 공개 애플리케이션을 위한 외부형으로 설정할 수 있습니다.  

---

## Security Considerations  
## 보안 고려사항  

Users can access your load balancer from anywhere using HTTP or HTTPS.  
사용자는 HTTP 또는 HTTPS를 통해 어디서든 로드 밸런서에 접근할 수 있습니다.  

Therefore, the security group rule for the load balancer typically allows inbound traffic on ports 80 or 443 from source 0.0.0.0/0 (anywhere).  
따라서 로드 밸런서의 보안 그룹 규칙은 일반적으로 0.0.0.0/0(모든 곳)에서 포트 80 또는 443으로의 인바운드 트래픽을 허용합니다.  

However, EC2 instances should only allow traffic originating from the load balancer.  
하지만 EC2 인스턴스는 로드 밸런서에서 오는 트래픽만 허용해야 합니다.  

Thus, the security group rule for EC2 instances allows HTTP traffic on port 80, but the source is restricted to the security group of the load balancer.  
따라서 EC2 인스턴스의 보안 그룹 규칙은 포트 80의 HTTP 트래픽을 허용하되, 출발지를 로드 밸런서의 보안 그룹으로 제한합니다.  

This linkage ensures that EC2 instances only accept traffic coming from the load balancer, enhancing security.  
이렇게 연결하면 EC2 인스턴스는 로드 밸런서에서 오는 트래픽만 수락하게 되어 보안이 강화됩니다.  

---

## Conclusion  
## 결론  

This overview covered the fundamentals of load balancers.  
이 개요에서는 로드 밸런서의 기본을 다루었습니다.  

In this section, we will discuss classic, application, and network load balancers in more detail in upcoming lectures.  
다음 강의에서는 CLB, ALB, NLB를 더 자세히 다룰 것입니다.  

---

## Key Takeaways  
## 핵심 요약  

- Load balancers distribute incoming traffic across multiple backend EC2 instances to ensure efficient resource use and reliability.  
- 로드 밸런서는 트래픽을 여러 EC2 인스턴스로 분산하여 자원 활용과 안정성을 보장합니다.  

- Elastic Load Balancers provide a single endpoint for users, handle health checks, SSL termination, and support high availability.  
- ELB는 단일 접속 지점을 제공하고, 헬스 체크와 SSL 종료, 고가용성을 지원합니다.  

- AWS offers four types of managed load balancers: Classic Load Balancer (deprecated), Application Load Balancer, Network Load Balancer, and Gateway Load Balancer.  
- AWS는 네 가지 관리형 로드 밸런서를 제공합니다: CLB(사용 중단), ALB, NLB, GWLB.  

- Security groups should be configured to allow user traffic to the load balancer and restrict EC2 instance traffic to only originate from the load balancer's security group.  
- 보안 그룹은 사용자 트래픽을 로드 밸런서로 허용하고, EC2 인스턴스는 로드 밸런서 보안 그룹에서 오는 트래픽만 허용해야 합니다.  
