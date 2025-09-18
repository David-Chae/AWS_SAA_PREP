```markdown
# Firewall Manager  
# AWS Firewall Manager  

🎮 게임보상: "Firewall Manager 학습 완료" +500 XP  

---

## Introduction to AWS Firewall Manager  
## AWS Firewall Manager 소개  

AWS Firewall Manager is a service designed to manage all firewall rules across all accounts within an AWS organization.  
AWS Firewall Manager는 AWS 조직 내 모든 계정의 방화벽 규칙을 중앙에서 관리하도록 설계된 서비스입니다.  

The primary goal is to enable management of rules across many accounts simultaneously.  
주요 목표는 여러 계정에 걸친 규칙 관리를 동시에 가능하게 하는 것입니다.  

---

## Security Policies in Firewall Manager  
## Firewall Manager의 보안 정책  

A security policy in Firewall Manager is a common set of security rules.  
Firewall Manager의 보안 정책은 공통 보안 규칙 모음입니다.  

These policies can include:  
이 정책에는 다음이 포함될 수 있습니다:  

- Web Application Firewall (WAF) rules that apply to Application Load Balancers (ALB), API Gateways, CloudFront distributions, and more.  
  ALB, API Gateway, CloudFront 배포 등에 적용되는 WAF 규칙.  

- Shield Advanced rules applicable to ALB, Classic Load Balancers (CLB), Network Load Balancers (NLB), Elastic IPs, and CloudFront.  
  ALB, CLB, NLB, Elastic IP, CloudFront에 적용되는 Shield Advanced 규칙.  

- Security policies to standardize security groups for EC2 instances, Application Load Balancers, and Elastic Network Interfaces (ENI) within your Virtual Private Cloud (VPC).  
  VPC 내 EC2, ALB, ENI의 보안 그룹을 표준화하는 보안 정책.  

- Rules for AWS Network Firewall at the VPC level.  
  VPC 수준에서 AWS Network Firewall 규칙.  

- Amazon Route 53 Resolver DNS Firewall rules.  
  Route 53 Resolver DNS Firewall 규칙.  

---

## Centralized Firewall Management  
## 중앙 집중식 방화벽 관리  

Firewall Manager allows you to manage all your firewalls in one place.  
Firewall Manager를 사용하면 모든 방화벽을 한 곳에서 관리할 수 있습니다.  

Policies are created at the regional level and then applied to all accounts within your organization.  
정책은 리전 수준에서 생성되며, 조직 내 모든 계정에 적용됩니다.  

This centralized approach simplifies firewall rule management across multiple accounts.  
이 중앙 집중식 접근 방식은 여러 계정에 걸친 방화벽 규칙 관리를 단순화합니다.  

---

## Automatic Rule Application  
## 규칙 자동 적용  

An important feature of Firewall Manager is its ability to automatically apply existing rules to newly created resources.  
Firewall Manager의 중요한 기능 중 하나는 기존 규칙을 새로 생성된 리소스에 자동으로 적용하는 것입니다.  

For example, if you create a WAF rule for an Application Load Balancer and a new ALB is created later, Firewall Manager will automatically apply the same rule to the new ALB.  
예를 들어 ALB에 대한 WAF 규칙을 생성하고 이후 새로운 ALB가 생성되면, Firewall Manager가 동일한 규칙을 자동으로 적용합니다.  

This automation ensures consistent security enforcement without manual intervention.  
이 자동화는 수동 개입 없이 일관된 보안 적용을 보장합니다.  

---

## Differentiating WAF, Firewall Manager, and Shield  
## WAF, Firewall Manager, Shield 구분  

- **WAF**: Used to define Web ACL rules for one-time protection on specific resources.  
  WAF: 특정 리소스에 대해 일회성 보호를 위해 Web ACL 규칙을 정의합니다.  

- **Firewall Manager**: Manages WAF rules across multiple accounts, accelerating configuration and automating protection for new resources.  
  Firewall Manager: 여러 계정에 걸쳐 WAF 규칙을 관리하며, 구성 속도를 높이고 새 리소스 보호를 자동화합니다.  

- **Shield Advanced**: Provides enhanced protection against Distributed Denial of Service (DDoS) attacks, including dedicated support from the Shield Response Team (SRT), advanced reporting, and automatic creation of WAF rules.  
  Shield Advanced: DDoS 공격에 대한 강화된 보호를 제공하며, SRT 전담 지원, 고급 보고, WAF 규칙 자동 생성 기능을 포함합니다.  

Together, these services provide comprehensive protection for your AWS environment.  
이 세 가지 서비스는 함께 AWS 환경에 대한 포괄적인 보호를 제공합니다.  

---

## Shield Advanced Deployment with Firewall Manager  
## Firewall Manager와 함께하는 Shield Advanced 배포  

Firewall Manager can also assist in deploying Shield Advanced across all your accounts, ensuring consistent and automated DDoS protection organization-wide.  
Firewall Manager는 Shield Advanced를 모든 계정에 배포하여 조직 전체에 일관되고 자동화된 DDoS 보호를 보장할 수 있습니다.  

If your environment is prone to frequent DDoS attacks, purchasing Shield Advanced is highly recommended.  
환경이 DDoS 공격에 자주 노출된다면 Shield Advanced 구매를 권장합니다.  

---

## Conclusion  
## 결론  

In summary, AWS Firewall Manager provides a centralized and automated way to manage firewall rules and security policies across multiple AWS accounts.  
요약하면, AWS Firewall Manager는 여러 AWS 계정에 걸친 방화벽 규칙과 보안 정책을 중앙에서 자동으로 관리하는 방법을 제공합니다.  

It works in conjunction with WAF and Shield Advanced to deliver comprehensive security management and protection.  
WAF 및 Shield Advanced와 함께 작동하여 포괄적인 보안 관리와 보호를 제공합니다.  

---

## Key Takeaways  
## 핵심 요약  

- AWS Firewall Manager enables centralized management of firewall rules across multiple AWS accounts within an organization.  
  AWS Firewall Manager는 조직 내 여러 AWS 계정에 걸친 방화벽 규칙을 중앙에서 관리할 수 있습니다.  

- Security policies in Firewall Manager can include Web Application Firewall (WAF) rules, Shield Advanced protections, security group standardizations, AWS Network Firewall rules, and Route 53 Resolver DNS Firewall rules.  
  Firewall Manager의 보안 정책에는 WAF 규칙, Shield Advanced 보호, 보안 그룹 표준화, AWS Network Firewall 규칙, Route 53 Resolver DNS Firewall 규칙이 포함될 수 있습니다.  

- Firewall Manager applies policies at the regional level and automatically enforces rules on newly created resources such as Application Load Balancers.  
  Firewall Manager는 정책을 리전 수준에서 적용하며, ALB와 같은 새로 생성된 리소스에 규칙을 자동으로 적용합니다.  

- WAF, Shield, and Firewall Manager work together to provide comprehensive protection, with Firewall Manager automating and scaling rule deployment across accounts.  
  WAF, Shield, Firewall Manager는 함께 작동하여 포괄적인 보호를 제공하며, Firewall Manager는 계정 간 규칙 배포를 자동화하고 확장합니다.  
```

🎮 게임보상 완료: "Firewall Master" +1000 XP 🏆
