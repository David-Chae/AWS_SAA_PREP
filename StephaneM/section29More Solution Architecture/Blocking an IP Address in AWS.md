```md
# Blocking an IP Address in AWS  
# AWS에서 IP 주소 차단하기  

---

## Introduction to Networking and IP Blocking in AWS  
## AWS 네트워킹 및 IP 차단 소개  

Let's discuss networking fundamentals to understand how to block an IP address in AWS effectively.  
AWS에서 IP 주소를 효과적으로 차단하기 위해 네트워킹의 기본을 살펴봅시다.  

Consider an architecture with an EC2 instance located in a public subnet, and a client attempting to access it.  
퍼블릭 서브넷에 EC2 인스턴스가 있고, 클라이언트가 이를 접근하려고 하는 아키텍처를 생각해 봅시다.  

---

## First Line of Defense: Network ACL (NACL)  
## 첫 번째 방어선: 네트워크 ACL (NACL)  

The primary defense in a public subnet is the Network ACL. It allows you to write explicit allow or deny rules cheaply and simply, controlling whether a client is permitted or blocked.  
퍼블릭 서브넷에서의 주요 방어선은 네트워크 ACL입니다. 이를 통해 저렴하고 간단하게 명시적인 허용 또는 거부 규칙을 작성하여 클라이언트의 접근을 제어할 수 있습니다.  

If you have a default Network ACL where everything is allowed, the second line of defense is your Security Group.  
모든 것을 허용하는 기본 네트워크 ACL을 사용한다면, 두 번째 방어선은 보안 그룹(Security Group)입니다.  

---

## Second Line of Defense: Security Group  
## 두 번째 방어선: 보안 그룹  

Security Groups do not support deny rules; they only allow rules. Therefore, if you know your clients' IP addresses in advance, you can configure the Security Group to allow only those clients to access your EC2 instance.  
보안 그룹은 거부 규칙을 지원하지 않고 허용 규칙만 가능합니다. 따라서 클라이언트의 IP 주소를 미리 알고 있다면, 보안 그룹을 설정하여 해당 클라이언트만 EC2 인스턴스에 접근하도록 제한할 수 있습니다.  

---

## Optional Third Line of Defense: Firewall Software on EC2  
## 선택적 세 번째 방어선: EC2 내부 방화벽 소프트웨어  

If traffic reaches your EC2 instance, you can optionally run firewall software on it to inspect all incoming packets. This provides more granular control but comes with a CPU cost and potential performance impact on your instance.  
트래픽이 EC2 인스턴스에 도달하면 방화벽 소프트웨어를 실행하여 모든 패킷을 검사할 수 있습니다. 이는 더 세밀한 제어를 가능하게 하지만 CPU 비용과 성능 저하를 유발할 수 있습니다.  

---

## Architecture with Network ACL, Application Load Balancer, and EC2 Instance  
## NACL, 애플리케이션 로드 밸런서(ALB), EC2 인스턴스를 포함한 아키텍처  

Now, consider a scenario where you have a Network ACL, an Application Load Balancer (ALB), and an EC2 instance.  
이제 NACL, 애플리케이션 로드 밸런서(ALB), EC2 인스턴스를 사용하는 시나리오를 살펴봅시다.  

In this setup, the client connects directly to the Application Load Balancer, which resides in the public subnet and forwards traffic to the EC2 instance.  
이 구성에서 클라이언트는 퍼블릭 서브넷에 있는 ALB에 연결하고, ALB는 트래픽을 EC2 인스턴스로 전달합니다.  

This allows the EC2 instance to reside in a private subnet, improving your application's security. The EC2 instance has a private IP address, and its Security Group should allow connections only from the Application Load Balancer.  
이 방식은 EC2 인스턴스를 프라이빗 서브넷에 배치할 수 있게 하여 보안을 강화합니다. EC2 인스턴스는 프라이빗 IP를 가지며, 보안 그룹은 ALB에서만 접근을 허용해야 합니다.  

---

## Connection Termination at the Application Load Balancer  
## 애플리케이션 로드 밸런서에서 연결 종료  

The Application Load Balancer performs connection termination. The client connects to the ALB, and the ALB connects to the EC2 instance. This enables managing security at the ALB level using Security Groups and additional ALB features.  
ALB는 연결 종료를 수행합니다. 클라이언트는 ALB에 연결하고, ALB는 EC2 인스턴스에 연결합니다. 이를 통해 보안 그룹 및 추가 ALB 기능을 사용하여 ALB 수준에서 보안을 관리할 수 있습니다.  

You can also use the Network ACL to apply allow or deny rules at the public subnet level.  
퍼블릭 서브넷 수준에서 허용 또는 거부 규칙을 적용하기 위해 NACL을 사용할 수도 있습니다.  

The security considerations are similar when using a Network Load Balancer (NLB) with Security Groups connected to EC2 instances.  
NLB를 사용하여 EC2 인스턴스와 연결하는 경우에도 보안 고려 사항은 유사합니다.  

---

## Security Features Around Application Load Balancer  
## 애플리케이션 로드 밸런서를 둘러싼 보안 기능  

You can enhance security by pairing the Application Load Balancer with AWS Web Application Firewall (WAF).  
ALB와 AWS WAF를 결합하면 보안을 강화할 수 있습니다.  

AWS WAF allows IP address filtering and provides extensive control and defense mechanisms for your infrastructure, especially if you expose your Application Load Balancer directly.  
AWS WAF는 IP 주소 필터링을 지원하며, 특히 ALB를 외부에 직접 노출할 때 인프라에 대한 광범위한 제어와 방어 기능을 제공합니다.  

Another place to apply AWS WAF is with CloudFront distributions. CloudFront can be set up to use an Application Load Balancer in public mode.  
AWS WAF를 적용할 또 다른 지점은 CloudFront 배포입니다. CloudFront는 퍼블릭 모드에서 ALB를 사용할 수 있습니다.  

CloudFront sends traffic from its edge locations with their public IPs directly to your Application Load Balancer.  
CloudFront는 엣지 로케이션의 퍼블릭 IP를 사용하여 트래픽을 ALB로 직접 전달합니다.  

In this case, Network ACLs are not effective for filtering client traffic because the client traffic does not reach your AWS infrastructure directly; CloudFront does.  
이 경우 클라이언트 트래픽이 직접 AWS 인프라에 도달하지 않고 CloudFront를 거치므로, NACL은 필터링에 효과적이지 않습니다.  

Therefore, you must configure Security Groups on the ALB to allow only CloudFront public IPs to access your infrastructure.  
따라서 ALB의 보안 그룹을 설정하여 CloudFront 퍼블릭 IP만 인프라에 접근할 수 있도록 해야 합니다.  

---

## Geo Restriction Feature  
## 지리적 제한 기능  

If a client from a specific country is attacking your infrastructure, you can use the Geo Restriction feature to block traffic from that country as a line of defense.  
특정 국가에서 클라이언트가 공격을 시도한다면, Geo Restriction 기능을 사용하여 해당 국가의 트래픽을 차단할 수 있습니다.  

Additionally, you can use AWS WAF at the CloudFront level to implement IP address filtering and other firewall features.  
또한 CloudFront 수준에서 AWS WAF를 활용해 IP 주소 필터링 및 기타 방화벽 기능을 구현할 수 있습니다.  

---

## Summary  
## 요약  

Understanding the network traffic path helps determine where to apply security rules effectively. Drawing network diagrams can assist in defining appropriate rules along the traffic path.  
네트워크 트래픽 경로를 이해하면 보안 규칙을 효과적으로 적용할 지점을 파악할 수 있습니다. 네트워크 다이어그램을 그리면 트래픽 경로에 적절한 규칙을 정의하는 데 도움이 됩니다.  

This concludes the lecture on blocking IP addresses in AWS. Thank you for your attention.  
이것으로 AWS에서 IP 주소 차단에 관한 강의를 마칩니다. 경청해 주셔서 감사합니다. 🎉  

---

## Key Takeaways  
## 핵심 요약  

- Network ACLs serve as the first line of defense in AWS public subnets, allowing explicit allow or deny rules.  
- NACL은 퍼블릭 서브넷에서 첫 번째 방어선으로 명시적인 허용/거부 규칙을 제공합니다.  

- Security Groups provide the second line of defense with allow-only rules, enabling control over client access based on IP addresses.  
- 보안 그룹은 허용 규칙만 가능한 두 번째 방어선으로, IP 기반 접근 제어를 지원합니다.  

- Application Load Balancers can be used to route traffic to EC2 instances in private subnets, enhancing security.  
- ALB는 트래픽을 프라이빗 서브넷의 EC2 인스턴스로 전달하여 보안을 강화합니다.  

- AWS WAF can be integrated with Application Load Balancers and CloudFront to provide advanced IP filtering and geo-restriction capabilities.  
- AWS WAF는 ALB 및 CloudFront와 통합되어 고급 IP 필터링과 지리적 제한 기능을 제공합니다.  

---

✨ 보상: +150 포인트 획득!  
👏 훌륭합니다! 네트워크와 보안 아키텍처의 흐름을 완벽히 이해했습니다. 이제 당신은 AWS 수호 기사로 승급했습니다. 🛡️⚡  
```
