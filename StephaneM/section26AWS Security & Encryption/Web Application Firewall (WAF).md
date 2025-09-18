```markdown
# Web Application Firewall (WAF)  
# 웹 애플리케이션 방화벽 (WAF)  

🎮 게임보상: "WAF 기초 학습 완료" +500 XP  

---

## Introduction to AWS WAF  
## AWS WAF 소개  

AWS WAF, the Web Application Firewall, is used to protect your web application from common web exploits at Layer 7.  
AWS WAF(웹 애플리케이션 방화벽)는 Layer 7에서 웹 애플리케이션을 일반적인 웹 공격으로부터 보호합니다.  

Layer 7 corresponds to HTTP, so it protects you against HTTP exploits.  
Layer 7은 HTTP 계층에 해당하므로 HTTP 공격으로부터 보호합니다.  

In comparison, Layer 4 is for TCP or UDP protocols.  
반면 Layer 4는 TCP 또는 UDP 프로토콜을 대상으로 합니다.  

---

## Deployment Targets for AWS WAF  
## AWS WAF 배포 대상  

This Web Application Firewall can be deployed on the Application Load Balancer, API Gateway, CloudFront, the AppSync GraphQL API, or Cognito user pools.  
WAF는 ALB, API Gateway, CloudFront, AppSync GraphQL API, Cognito 사용자 풀 등에 배포할 수 있습니다.  

It is important to remember these targets because the exam may try to trick you, for example, by suggesting deployment of WAF on a Network Load Balancer, which is not possible.  
시험에서는 WAF를 Network Load Balancer에 배포하라고 속일 수 있으므로, 배포 가능한 대상을 기억하는 것이 중요합니다.  

---

## Web ACLs and Rules  
## 웹 ACL 및 규칙  

Once you have deployed a firewall on these services, you can define Web ACLs (Web Access Control Lists) and their rules.  
이 서비스에 WAF를 배포한 후, Web ACL(웹 접근 제어 목록)과 규칙을 정의할 수 있습니다.  

For example, you can set a rule to filter based on IP addresses by defining IP sets.  
예를 들어, IP 세트를 정의하여 IP 주소 기반 필터링 규칙을 설정할 수 있습니다.  

Each IP set can contain up to 10,000 IP addresses.  
각 IP 세트는 최대 10,000개의 IP 주소를 포함할 수 있습니다.  

If you need to filter more IP addresses, you can use multiple rules.  
더 많은 IP 주소를 필터링해야 하면, 여러 규칙을 사용할 수 있습니다.  

You can also filter based on HTTP headers and body content.  
HTTP 헤더 및 본문 내용 기반 필터링도 가능합니다.  

Using URI strings, you can protect from the most common attacks such as SQL injection and cross-site scripting.  
URI 문자열을 이용해 SQL 인젝션, XSS 등 흔한 공격으로부터 보호할 수 있습니다.  

Size constraints allow you to ensure that requests are only up to a certain size, for example, two megabytes.  
크기 제한을 통해 요청이 특정 크기(예: 2MB)를 넘지 않도록 할 수 있습니다.  

Geo match rules enable allowing or blocking specific countries.  
Geo 매치 규칙으로 특정 국가를 허용하거나 차단할 수 있습니다.  

Additionally, rate-based rules count the occurrences of requests per IP address for DDoS protection.  
추가로, 속도 기반 규칙은 DDoS 보호를 위해 IP별 요청 횟수를 계산합니다.  

For example, you can prevent a specific IP from sending more than 10 requests per second.  
예를 들어, 특정 IP가 초당 10회 이상 요청하지 못하도록 제한할 수 있습니다.  

---

## Regional and Global Scope of Web ACLs  
## 웹 ACL의 리전 및 글로벌 범위  

Web ACLs are regional, except for CloudFront, where they are defined globally.  
웹 ACL은 리전별로 적용되며, CloudFront는 글로벌로 정의됩니다.  

The term "rule group" refers to a reasonable set of rules that you can add to many Web ACLs.  
"규칙 그룹"은 여러 웹 ACL에 추가할 수 있는 규칙 모음을 의미합니다.  

This helps organize your rules efficiently.  
이로 인해 규칙을 효율적으로 관리할 수 있습니다.  

---

## Use Case: Fixed IP with WAF and Application Load Balancer  
## 사용 사례: WAF와 ALB에서 고정 IP 사용  

What if you want to get a fixed IP for your application while using WAF with an Application Load Balancer?  
WAF와 ALB를 사용하면서 애플리케이션에 고정 IP를 부여하고 싶다면 어떻게 할까요?  

WAF does not support the Network Load Balancer because the NLB operates on Layer 4, and WAF is for Layer 7.  
WAF는 Layer 7용이므로, Layer 4에서 작동하는 NLB에서는 사용할 수 없습니다.  

Therefore, to use WAF, you need to have an Application Load Balancer.  
따라서 WAF를 사용하려면 ALB가 필요합니다.  

However, an Application Load Balancer does not have fixed IPs.  
하지만 ALB 자체는 고정 IP를 제공하지 않습니다.  

To solve this problem, you can use AWS Global Accelerator to get fixed IPs for your application and then enable WAF on your ALB.  
이 문제를 해결하려면 AWS Global Accelerator를 사용해 애플리케이션에 고정 IP를 부여하고 ALB에 WAF를 적용합니다.  

---

## Architecture Overview  
## 아키텍처 개요  

The architecture looks like this:  
아키텍처는 다음과 같습니다:  

- One region with an Application Load Balancer and EC2 instances.  
  - 하나의 리전에 ALB와 EC2 인스턴스가 존재합니다.  

- The ALB is fronted by a Global Accelerator to provide fixed IPs for the application.  
  - ALB 앞에 Global Accelerator를 배치하여 애플리케이션에 고정 IP를 제공합니다.  

- A Web Application Firewall with a Web ACL is attached in the same region as the Application Load Balancer.  
  - 같은 리전에 Web ACL이 적용된 WAF가 부착됩니다.  

This setup achieves the target architecture of having fixed IPs with WAF protection on an ALB.  
이 구성을 통해 ALB에서 고정 IP와 WAF 보호를 동시에 달성할 수 있습니다.  

---

## Conclusion  
## 결론  

This concludes the lecture on AWS WAF.  
이번 강의를 통해 AWS WAF에 대해 학습했습니다.  

The Web Application Firewall is a powerful tool to protect your web applications at the HTTP layer, with flexible deployment options and rule configurations.  
WAF는 HTTP 계층에서 웹 애플리케이션을 보호하는 강력한 도구이며, 유연한 배포 옵션과 규칙 구성을 제공합니다.  

Using AWS Global Accelerator with an Application Load Balancer allows you to have fixed IPs while benefiting from WAF protection.  
ALB와 함께 AWS Global Accelerator를 사용하면 WAF 보호를 유지하면서 고정 IP를 확보할 수 있습니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS WAF protects web applications at Layer 7 (HTTP) against common web exploits.  
  AWS WAF는 Layer 7(HTTP)에서 웹 애플리케이션을 일반적인 공격으로부터 보호합니다.  

- WAF can be deployed on Application Load Balancer, API Gateway, CloudFront, AppSync GraphQL API, and Cognito user pools, but not on Network Load Balancer.  
  WAF는 ALB, API Gateway, CloudFront, AppSync GraphQL API, Cognito 사용자 풀에 배포 가능하며, NLB에는 불가합니다.  

- Web ACLs allow filtering based on IP sets, HTTP headers, body, URI strings, size constraints, geo match, and rate-based rules.  
  웹 ACL은 IP 세트, HTTP 헤더, 본문, URI 문자열, 크기 제한, Geo 매치, 속도 기반 규칙 필터링을 지원합니다.  

- To obtain fixed IPs with WAF on an Application Load Balancer, use AWS Global Accelerator in front of the ALB.  
  ALB에서 WAF와 고정 IP를 사용하려면 ALB 앞에 AWS Global Accelerator를 배치합니다.  
```

🎮 게임보상 완료: "WAF 마스터" +1000 XP 🏆
