```markdown
# DDoS Protection Best Practices  
# DDoS 보호 모범 사례  

🎮 게임보상: "DDoS Protection Expert" +500 XP  

---

## Introduction to DDoS Protection Architecture  
## DDoS 보호 아키텍처 소개  

This lecture focuses on solution architecture related to DDoS protection and best practices.  
이번 강의는 DDoS 보호와 관련된 솔루션 아키텍처 및 모범 사례에 중점을 둡니다.  

Consider an architecture where an auto scaling group with EC2 instances is fronted by an Elastic Load Balancer (ELB).  
EC2 인스턴스를 가진 오토스케일링 그룹이 ELB(Elastic Load Balancer) 뒤에 배치된 아키텍처를 생각해 보세요.  

The load balancer can be exposed through a Global Accelerator providing fixed IPs or fronted by CloudFront distributions.  
로드 밸런서는 고정 IP를 제공하는 Global Accelerator를 통해 노출되거나 CloudFront 배포 앞에 배치될 수 있습니다.  

CloudFront can be linked to a Web Application Firewall (WAF) for additional protection.  
CloudFront는 추가 보호를 위해 WAF(Web Application Firewall)와 연결될 수 있습니다.  

Route 53 can be used for DNS routing.  
DNS 라우팅에는 Route 53을 사용할 수 있습니다.  

Another architecture variation includes CloudFront combined with API Gateway.  
또 다른 아키텍처 변형은 CloudFront와 API Gateway의 조합입니다.  

These combinations illustrate various approaches to DDoS resiliency.  
이러한 조합은 DDoS 복원력을 위한 다양한 접근 방식을 보여줍니다.  

---

## Edge Location Mitigation  
## 엣지 위치 기반 완화  

Using CloudFront places your web application delivery at the Edge, providing protection against common DDoS attacks such as SYN floods and UDP reflection through AWS Shield.  
CloudFront를 사용하면 웹 애플리케이션 전달이 엣지에서 이루어져, SYN 플러드, UDP 반사 공격과 같은 일반 DDoS 공격으로부터 AWS Shield를 통해 보호됩니다.  

Similarly, Global Accelerator enables global access to your application at the Edge and integrates fully with Shield for DDoS protection.  
마찬가지로 Global Accelerator는 엣지에서 애플리케이션에 글로벌 접근을 가능하게 하고 Shield와 완전히 통합되어 DDoS 보호를 제공합니다.  

This is particularly useful if your backend is not compatible with CloudFront.  
백엔드가 CloudFront와 호환되지 않는 경우 특히 유용합니다.  

Whether using CloudFront or Global Accelerator, your application benefits from distributed Edge locations with built-in DDoS protection.  
CloudFront든 Global Accelerator든, 분산된 엣지 위치에서 내장 DDoS 보호를 통해 애플리케이션이 보호됩니다.  

Additionally, Route 53 offers global domain name resolution with DDoS protection mechanisms on DNS queries.  
또한 Route 53은 DNS 쿼리에 대한 DDoS 보호 메커니즘과 함께 글로벌 도메인 이름 해석을 제공합니다.  

Overall, operating at the Edge enhances DDoS defense capabilities.  
전반적으로 엣지에서 운영하면 DDoS 방어 능력이 향상됩니다.  

---

## Infrastructure Layer Defense  
## 인프라 계층 방어  

Best practices BP1, BP3, and BP6 focus on infrastructure layer defense.  
모범 사례 BP1, BP3, BP6은 인프라 계층 방어에 중점을 둡니다.  

By leveraging CloudFront, Global Accelerator, Route 53, and Elastic Load Balancing, Amazon EC2 instances are shielded from high traffic volumes.  
CloudFront, Global Accelerator, Route 53, ELB를 활용하면 EC2 인스턴스가 높은 트래픽으로부터 보호됩니다.  

These services handle most traffic before it reaches EC2 instances.  
이 서비스들은 대부분의 트래픽을 EC2 인스턴스에 도달하기 전에 처리합니다.  

Enabling auto-scaling on EC2 instances allows automatic scaling to accommodate increased load.  
EC2 인스턴스에서 오토스케일링을 활성화하면 증가된 부하를 자동으로 처리할 수 있습니다.  

Elastic Load Balancing distributes traffic evenly across multiple EC2 instances, ensuring each instance manages a reasonable amount of traffic, assuming the auto-scaling group has scaled accordingly.  
ELB는 트래픽을 여러 EC2 인스턴스에 고르게 분배하여 각 인스턴스가 합리적인 트래픽을 처리하도록 보장합니다. 오토스케일링 그룹이 확장되었다고 가정합니다.  

---

## Application Layer Defense  
## 애플리케이션 계층 방어  

At the application layer, best practices BP1 and BP2 involve detecting and filtering malicious requests.  
애플리케이션 계층에서는 BP1, BP2가 악성 요청을 탐지하고 필터링하는 것을 포함합니다.  

CloudFront serves static content from Edge locations, protecting the backend.  
CloudFront는 엣지 위치에서 정적 콘텐츠를 제공하여 백엔드를 보호합니다.  

WAF can be deployed on CloudFront or application load balancers to filter and block requests based on signatures, such as specific IP addresses or request types.  
WAF는 CloudFront 또는 ALB에 배치하여 특정 IP나 요청 유형 같은 시그니처를 기반으로 요청을 필터링하고 차단할 수 있습니다.  

WAF rate-based rules enable automatic blocking of IPs exhibiting malicious behavior.  
WAF의 비율 기반 규칙은 악성 행동을 보이는 IP를 자동으로 차단할 수 있습니다.  

Managed WAF rules can block IPs based on reputation or anonymity.  
관리형 WAF 규칙은 평판이나 익명성을 기반으로 IP를 차단할 수 있습니다.  

CloudFront also allows blocking requests from specific geographies.  
CloudFront는 특정 지리적 위치의 요청도 차단할 수 있습니다.  

These managed services help mitigate DDoS attacks effectively.  
이 관리형 서비스들은 DDoS 공격을 효과적으로 완화하는 데 도움을 줍니다.  

Enabling Shield Advanced further enhances protection by automatically creating WAF rules to mitigate layer seven attacks, minimizing bad requests to EC2 instances.  
Shield Advanced를 활성화하면 레이어 7 공격을 완화하기 위해 자동으로 WAF 규칙을 생성하여 EC2로 전달되는 악성 요청을 최소화하며 보호를 강화합니다.  

---

## Reducing Attack Surface  
## 공격 표면 감소  

Best practices BP1, BP4, and BP6 emphasize reducing the attack surface.  
BP1, BP4, BP6은 공격 표면을 줄이는 것에 중점을 둡니다.  

Backend AWS resources serving the application are hidden behind services such as CloudFront, API Gateway, or Elastic Load Balancing.  
애플리케이션을 제공하는 백엔드 AWS 리소스는 CloudFront, API Gateway, ELB 등의 서비스 뒤에 숨겨집니다.  

This obscures the nature of backend resources, whether Lambda functions, EC2 instances, or ECS tasks, from attackers.  
이를 통해 Lambda, EC2, ECS 태스크 등 백엔드 리소스의 특성을 공격자로부터 숨길 수 있습니다.  

Security groups and network ACLs can filter traffic based on specific IP addresses.  
보안 그룹과 네트워크 ACL은 특정 IP 주소를 기반으로 트래픽을 필터링할 수 있습니다.  

Elastic IPs, if used, can also be protected by AWS Shield Advanced.  
사용하는 Elastic IP도 AWS Shield Advanced로 보호할 수 있습니다.  

API Gateway protects API endpoints by hiding backend implementations.  
API Gateway는 백엔드 구현을 숨겨 API 엔드포인트를 보호합니다.  

Using Edge-optimized mode provides global access, while regional mode offers more control for DDoS protection.  
엣지 최적화 모드는 글로벌 접근을 제공하고, 리전 모드는 DDoS 보호에 대한 더 많은 제어를 제공합니다.  

WAF on API Gateway filters HTTP requests, and configuring API Gateway with burst limits, header filtering, and API keys further protects against DDoS attacks.  
API Gateway의 WAF는 HTTP 요청을 필터링하며, 버스트 제한, 헤더 필터링, API 키 설정으로 DDoS 공격에 대한 추가 보호가 가능합니다.  

---

## Conclusion  
## 결론  

This architecture demonstrates various ways to protect against DDoS attacks using AWS services.  
이 아키텍처는 AWS 서비스를 사용하여 DDoS 공격을 방어하는 다양한 방법을 보여줍니다.  

Understanding these best practices is essential for designing resilient applications and preparing for related exam questions.  
이 모범 사례를 이해하는 것은 복원력 있는 애플리케이션 설계와 관련 시험 준비에 필수적입니다.  

---

## Key Takeaways  
## 핵심 요약  

- Utilizing AWS Edge services like CloudFront, Global Accelerator, and Route 53 enhances DDoS protection by distributing traffic and filtering attacks at the network edge.  
  CloudFront, Global Accelerator, Route 53 같은 AWS 엣지 서비스를 활용하면 트래픽을 분산하고 네트워크 엣지에서 공격을 필터링하여 DDoS 보호를 강화할 수 있습니다.  

- Infrastructure layer defenses include auto-scaling EC2 instances and Elastic Load Balancing to manage high traffic and distribute load effectively.  
  인프라 계층 방어에는 오토스케일링 EC2 인스턴스와 ELB를 활용하여 높은 트래픽을 관리하고 부하를 효과적으로 분산하는 것이 포함됩니다.  

- Application layer defenses leverage CloudFront, WAF, and Shield Advanced to detect, filter, and block malicious requests, including rate-based blocking and geographic restrictions.  
  애플리케이션 계층 방어는 CloudFront, WAF, Shield Advanced를 활용하여 악성 요청을 탐지, 필터링, 차단하며, 비율 기반 차단 및 지리적 제한도 포함됩니다.  

- Reducing the attack surface by hiding backend resources behind services like API Gateway, CloudFront, and ELB, combined with security groups and network ACLs, strengthens overall DDoS resiliency.  
  API Gateway, CloudFront, ELB 뒤에 백엔드 리소스를 숨기고, 보안 그룹과 네트워크 ACL을 결합하여 공격 표면을 줄이면 전반적인 DDoS 복원력이 강화됩니다.  
```

🎮 게임보상 완료: "DDoS Protection Architect" +1000 XP 🏆
