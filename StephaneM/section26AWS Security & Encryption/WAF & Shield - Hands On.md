```markdown
# WAF & Shield - Hands On  
# WAF & Shield 실습  

🎮 게임보상: "WAF & Shield 실습 완료" +500 XP  

---

## Introduction to AWS WAF, Shield, and Firewall Manager  
## AWS WAF, Shield, Firewall Manager 소개  

In this session, we will explore AWS WAF, Shield, and Firewall Manager.  
이번 세션에서는 AWS WAF, Shield, 그리고 Firewall Manager를 살펴봅니다.  

These services help protect your web applications and manage security policies effectively.  
이 서비스들은 웹 애플리케이션을 보호하고 보안 정책을 효과적으로 관리하는 데 도움을 줍니다.  

When you access the AWS console and search for WAF and Shield, you arrive at a user interface that includes WAF on the left-hand side, Shield in the middle, and Firewall Manager on the right.  
AWS 콘솔에서 WAF와 Shield를 검색하면, 왼쪽에 WAF, 가운데에 Shield, 오른쪽에 Firewall Manager가 있는 UI를 볼 수 있습니다.  

---

## AWS WAF Overview  
## AWS WAF 개요  

AWS WAF helps protect your web applications from common web exploits at the layer seven level.  
AWS WAF는 레이어 7 수준에서 일반적인 웹 공격으로부터 웹 애플리케이션을 보호합니다.  

It is designed to safeguard resources such as your Amazon API Gateway, CloudFront distributions, or Application Load Balancers (ALB).  
API Gateway, CloudFront 배포, ALB와 같은 리소스를 보호하도록 설계되었습니다.  

---

## Creating a Web ACL  
## Web ACL 생성  

To use WAF, you create a Web Access Control List (Web ACL).  
WAF를 사용하려면 Web ACL(Web Access Control List)을 생성합니다.  

For example, you might name it Demo Web ACL.  
예를 들어, 이름을 "Demo Web ACL"로 지정할 수 있습니다.  

You then specify whether the Web ACL is for a regional resource, such as an ALB or API Gateway, or for a CloudFront distribution.  
그 다음 Web ACL이 ALB나 API Gateway와 같은 리전 리소스를 위한 것인지, CloudFront 배포를 위한 것인지 지정합니다.  

CloudFront Web ACLs are global and only available in the US East (N. Virginia) region.  
CloudFront Web ACL은 글로벌이며, US East (N. Virginia) 리전에서만 사용할 수 있습니다.  

For this demonstration, we select a regional resource and choose the Ireland region in Europe.  
이번 실습에서는 리전 리소스를 선택하고, 유럽의 Ireland 리전을 선택합니다.  

This Web ACL will be named Demo Web ACL.  
이 Web ACL의 이름은 "Demo Web ACL"입니다.  

---

## Associating Resources  
## 리소스 연결  

Next, you can associate AWS resources with the Web ACL to protect them.  
그 다음, Web ACL과 보호하려는 AWS 리소스를 연결할 수 있습니다.  

For example, you can add Application Load Balancers or API Gateways by selecting the appropriate resources from the list.  
예를 들어, 리스트에서 적절한 리소스를 선택해 ALB나 API Gateway를 추가할 수 있습니다.  

---

## Adding Rules  
## 규칙 추가  

You can add multiple rules to your Web ACL.  
Web ACL에 여러 규칙을 추가할 수 있습니다.  

These rules can be managed rule groups provided by AWS or partners, or you can create your own custom rules.  
규칙은 AWS 또는 파트너가 제공하는 관리형 규칙 그룹을 사용하거나, 커스텀 규칙을 생성할 수 있습니다.  

---

## Managed Rule Groups  
## 관리형 규칙 그룹  

AWS offers several managed rule groups, such as:  
AWS는 다음과 같은 관리형 규칙 그룹을 제공합니다:  

- Bot control rules to prevent bots from accessing your application.  
  봇 제어 규칙: 봇이 애플리케이션에 접근하지 못하도록 합니다.  

- Amazon IP reputation lists to allow access only from reputable IP addresses.  
  IP 평판 리스트: 신뢰할 수 있는 IP 주소만 접근 허용.  

- Rules to block anonymous IPs, including those coming from VPNs and proxies.  
  익명 IP 차단 규칙: VPN, 프록시 IP 포함.  

- Rules to block known bad inputs that are commonly used in attacks.  
  공격에 자주 사용되는 알려진 악성 입력 차단 규칙.  

You can add these rules to your Web ACL.  
이 규칙들을 Web ACL에 추가할 수 있습니다.  

Each rule has an associated capacity, with a maximum total capacity of 1500 to prevent overloading the Web ACL with too many rules.  
각 규칙에는 용량이 있으며, Web ACL 과부하를 방지하기 위해 최대 총 용량은 1500입니다.  

---

## Default Action  
## 기본 동작  

If a request does not match any of the rules, the default action is to allow the request.  
요청이 규칙과 일치하지 않으면 기본 동작은 허용입니다.  

Otherwise, the request will be blocked.  
그렇지 않으면 요청이 차단됩니다.  

---

## Rule Priorities and Metrics  
## 규칙 우선순위 및 지표  

You can set the priority order of rules, for example, deciding whether the bad inputs rule or the anonymous IP list rule is evaluated first.  
규칙의 우선순위를 설정할 수 있으며, 예를 들어, 악성 입력 규칙과 익명 IP 리스트 규칙 중 어떤 것을 먼저 평가할지 결정할 수 있습니다.  

Metrics are associated with each rule to monitor their activity.  
각 규칙에는 활동을 모니터링할 수 있는 지표가 연결됩니다.  

After configuring the rules and priorities, you can create the Web ACL.  
규칙과 우선순위를 구성한 후 Web ACL을 생성할 수 있습니다.  

Once created, it can be associated with your ALB, API Gateway, or other supported resources.  
생성 후 ALB, API Gateway 등 지원되는 리소스와 연결할 수 있습니다.  

---

## IP Sets  
## IP 세트  

Within WAF, you can also configure IP sets, which are lists of IP addresses that you want to explicitly allow or block.  
WAF에서 IP 세트를 구성할 수도 있습니다. IP 세트는 명시적으로 허용하거나 차단할 IP 주소 리스트입니다.  

These IP addresses are entered one per line in the specified format.  
IP 주소는 지정된 형식으로 한 줄씩 입력합니다.  

---

## AWS Shield Overview  
## AWS Shield 개요  

AWS Shield provides Distributed Denial of Service (DDoS) protection.  
AWS Shield는 분산 서비스 거부(DDoS) 공격으로부터 보호합니다.  

There is a standard version included with AWS services and an advanced version called Shield Advanced, which costs $3,000 per month.  
기본 버전은 AWS 서비스에 포함되며, 고급 버전인 Shield Advanced는 월 $3,000입니다.  

Shield Advanced offers enhanced DDoS protection, but subscribing to it incurs significant costs.  
Shield Advanced는 강화된 DDoS 보호를 제공하지만, 가입 시 상당한 비용이 발생합니다.  

It is recommended to be cautious and avoid experimenting with Shield Advanced without proper planning to prevent unexpected charges.  
예상치 못한 비용 발생을 막기 위해 계획 없이 Shield Advanced를 실험하는 것은 피하는 것이 좋습니다.  

---

## Firewall Manager Overview  
## Firewall Manager 개요  

Firewall Manager provides centralized security management for your AWS environment.  
Firewall Manager는 AWS 환경에 대한 중앙 집중식 보안 관리를 제공합니다.  

It allows you to create security policies that apply across multiple AWS accounts within your organization.  
조직 내 여러 계정에 걸쳐 적용되는 보안 정책을 생성할 수 있습니다.  

Creating a Firewall Manager policy costs $100 per month.  
Firewall Manager 정책 생성 비용은 월 $100입니다.  

These policies can manage WAF rules, Shield Advanced protections, security groups, network firewalls, and more across all accounts.  
이 정책들은 모든 계정에서 WAF 규칙, Shield Advanced 보호, 보안 그룹, 네트워크 방화벽 등을 관리할 수 있습니다.  

For example, you can create a WAF policy for the Ireland region that applies to all your AWS accounts.  
예를 들어, Ireland 리전에 대한 WAF 정책을 생성하여 모든 AWS 계정에 적용할 수 있습니다.  

This policy allows you to configure rules and other settings centrally.  
이 정책을 통해 규칙 및 기타 설정을 중앙에서 구성할 수 있습니다.  

---

## Conclusion  
## 결론  

These three services—WAF, Shield, and Firewall Manager—complement each other to provide comprehensive security for your AWS applications and infrastructure.  
이 세 가지 서비스(WAF, Shield, Firewall Manager)는 서로 보완하여 AWS 애플리케이션과 인프라에 포괄적인 보안을 제공합니다.  

WAF protects against common web exploits, Shield defends against DDoS attacks, and Firewall Manager centralizes security policy management.  
WAF는 일반 웹 공격을 방어하고, Shield는 DDoS 공격을 방어하며, Firewall Manager는 보안 정책 관리를 중앙에서 수행합니다.  

Thank you for following this session.  
이번 세션을 따라와 주셔서 감사합니다.  

I hope you found it informative, and I look forward to seeing you in the next lecture.  
유익한 시간이었기를 바라며, 다음 강의에서 뵙겠습니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS WAF protects web applications from common layer seven web exploits.  
  AWS WAF는 레이어 7의 일반적인 웹 공격으로부터 웹 애플리케이션을 보호합니다.  

- Web ACLs can be created and associated with regional or global resources like ALB, API Gateway, or CloudFront.  
  Web ACL은 ALB, API Gateway, CloudFront와 같은 리전 또는 글로벌 리소스에 생성 및 연결할 수 있습니다.  

- Managed rule groups help block threats such as anonymous IPs, bad inputs, and bots.  
  관리형 규칙 그룹은 익명 IP, 악성 입력, 봇과 같은 위협을 차단하는 데 도움을 줍니다.  

- AWS Shield provides DDoS protection, while Firewall Manager centralizes security management across accounts.  
  AWS Shield는 DDoS 보호를 제공하고, Firewall Manager는 계정 전반에 걸쳐 보안 관리를 중앙화합니다.  
```

🎮 게임보상 완료: "WAF & Shield Hands-On Master" +1000 XP 🏆
